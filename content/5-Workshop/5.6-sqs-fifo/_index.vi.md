---
title : "Amazon SQS FIFO"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---
#### Amazon SQS FIFO

#### 5.6.1 Khái niệm

**Amazon SQS FIFO (First-In-First-Out)** là một loại hàng đợi (queue) do AWS cung cấp, được thiết kế đặc biệt để đảm bảo hai yếu tố cực kỳ quan trọng trong các hệ thống phân tán: **thứ tự xử lý tin nhắn** và  **tránh trùng lặp dữ liệu** .

#### 5.6.2 Kiến trúc hệ thống

![1783096083070](image/_index.vi/1783096083070.png)

<div align="center"><i>Hình 5.6.1:Kiến trúc hệ thống.</i></div>

ví dụ với luồng xử lí POST /Economy/earn :

* Client gửi POST /Economy/earn.
* API Gateway chuyển request đến Producer Lambda.
* Producer Lambda tạo message và gửi vào Amazon SQS FIFO, không ghi trực tiếp vào cơ sở dữ liệu.
* Producer Lambda phản hồi ngay cho Client với trạng thái queued.
* Amazon SQS kích hoạt Consumer Lambda khi có message.
* Consumer Lambda mở transaction và sử dụng SELECT ... FOR UPDATE để khóa bản ghi, tránh xung đột dữ liệu.
* Consumer Lambda xử lý nghiệp vụ và ghi dữ liệu vào Amazon Aurora/RDS.
* Sau khi xử lý thành công, message được xóa khỏi SQS; nếu thất bại sẽ được retry hoặc chuyển sang DLQ.

#### 5.6.3 Setup SQS FIFO

##### * Tạo FIFO Queue

Định nghĩa queue trong services/sqs-infrastructure/serverless.yml:

```YAML
EconomyQueue:
  Type: AWS::SQS::Queue
  Properties:
    QueueName: game-economy.fifo
    FifoQueue: true
    ContentBasedDeduplication: true    # SQS tự động dedup dựa trên nội dung
    VisibilityTimeout: 60              # 60s cho consumer xử lý
    MessageRetentionPeriod: 345600     # 4 ngày
    RedrivePolicy:
      deadLetterTargetArn: !GetAtt EconomyDLQ.Arn
      maxReceiveCount: 3               # Retry 3 lần rồi chuyển DLQ
```

##### * Khởi tạo SQS Consumer Lambda

![1783405716023](image/_index.vi/1783405716023.png)

<div align="center"><i>Hình 5.6.2:Hệ thống SQS Consumer Lambda .</i></div>

##### * Cấu hình IAM

File .env cho local development:

```
AWS_REGION=ap-southeast-1
AWS_ENDPOINT_URL=http://localhost:4566
ECONOMY_QUEUE_URL=http://sqs.ap-southeast-1.localhost.localstack.cloud:4566/000000000000/game-economy.fifo
INVENTORY_QUEUE_URL=http://sqs.ap-southeast-1.localhost.localstack.cloud:4566/000000000000/game-inventory.fifo
GIFTCODE_QUEUE_URL=http://sqs.ap-southeast-1.localhost.localstack.cloud:4566/000000000000/game-giftcode.fifo
STATS_QUEUE_URL=http://sqs.ap-southeast-1.localhost.localstack.cloud:4566/000000000000/game-stats.fifo
SAVE_DATA_QUEUE_URL=http://sqs.ap-southeast-1.localhost.localstack.cloud:4566/000000000000/game-save-data.fifo
```

Thêm policy mới:

![1783404285339](image/_index.vi/1783404285339.png)

<div align="center"><i>Hình 5.6.3:Thêm policy mới để cấp role khởi tạo sqs.</i></div>

```YAML
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": [
				"cloudformation:*",
				"sqs:*",
				"s3:*",
				"lambda:*",
				"logs:*",
				"iam:CreateRole",
				"iam:DeleteRole",
				"iam:GetRole",
				"iam:PutRolePolicy",
				"iam:DeleteRolePolicy",
				"iam:AttachRolePolicy",
				"iam:DetachRolePolicy"
			],
			"Resource": "*"
		},
		{
			"Effect": "Allow",
			"Action": "iam:PassRole",
			"Resource": "*",
			"Condition": {
				"StringEquals": {
					"iam:PassedToService": "cloudformation.amazonaws.com"
				}
			}
		}
	]
}
```

**Producer IAM** (trong services/lambda-economy/serverless.yml):

```yaml
iamRoleStatements:
  - Effect: Allow
    Action: [sqs:SendMessage]
    Resource: !ImportValue EconomyQueueArn
```

**Consumer IAM** (trong services/sqs-consumer-economy/serverless.yml):

```yaml
iamRoleStatements:
  - Effect: Allow
    Action: [sqs:ReceiveMessage, sqs:DeleteMessage, sqs:GetQueueAttributes]
    Resource: !ImportValue EconomyQueueArn
```

##### * Kết nối Producer

Shared SQS client (shared/src/sqs/producer.ts):

```typescript
const client = new SQSClient({
  region: process.env.AWS_REGION || 'ap-southeast-1',
  endpoint: process.env.AWS_ENDPOINT_URL || undefined,  // LocalStack support
});
```

Message gửi lên queue gồm:

- MessageGroupId: account_{accountId} (hoặc giftcode_{code})
- MessageDeduplicationId: tự gen từ {type}_{entityId}_{timestamp}_{random}
- MessageBody: JSON chứa type, payload, timestamp, requestId

Dùng SqsProducer class trong controller:

```typescript
// EconomyController.earnCurrency
const messageId = await SqsProducer.economyEarn({
  accountId,
  currencyType: 'coin',
  amount: 100,
});
res.status(202).json({ success: true, status: 'queued', requestId: messageId });
```

##### * Tạo Consumer Lambda

File services/sqs-consumer-economy/serverless.yml:

```yaml
functions:
  consumer:
    handler: src/lambda.handler
    timeout: 60
    memorySize: 256
    events:
      - sqs:
          arn: !ImportValue EconomyQueueArn
          batchSize: 1                    # FIFO bắt buộc batchSize = 1
          maximumConcurrency: 2
          functionResponseType: ReportBatchItemFailures
```

Handler pattern (services/sqs-consumer-economy/src/lambda.ts):

```typescript
export const handler = async (event: SQSEvent): Promise<SQSBatchResponse> => {
  if (!initialized) {          
    await initializeApplicationDbContext();
    initialized = true;
  }
  const batchItemFailures: { itemIdentifier: string }[] = [];
  for (const record of event.Records) {
    try {
      const message: SQSMessage = JSON.parse(record.body);
      switch (message.type) {  
        case 'economy.earn':
          await handleEarnCurrency(message.payload);
          break;
        case 'economy.spend':
          await handleSpendCurrency(message.payload);
          break;
      }
    } catch (error) {
      batchItemFailures.push({ itemIdentifier: record.messageId });
    }
  }
  return { batchItemFailures };
};
```

Xử lý với pessimistic lock trong handler:

```typescript
await ApplicationDbContext.manager.transaction(async (manager) => {
  const wallet = await manager.findOne(UserCurrency, {
    where: { accountId: payload.accountId },
    lock: { mode: 'pessimistic_write' },  
  });
  wallet.coin += payload.amount;
  await manager.save(wallet);
});
```

##### * Deploy SQS Infrastructure

```
cd services/sqs-infrastructure
serverless deploy --stage dev
```

Stack tên gameapi-sqs-infrastructure-dev, sẽ tạo:

- 5 FIFO queues (game-economy.fifo, game-inventory.fifo, game-giftcode.fifo, game-stats.fifo, game-save-data.fifo)

![1783403865434](image/_index.vi/1783403865434.png)

<div align="center"><i>Hình 5.6.4: Deploy SQS thành công.</i></div>

chú thích : các file dlq có trong queues sẽ được hướng dẫn setup và deploy ở phần 5.7 AWS SQS Dead Letter Queue

##### * Deploy consumer sqs

ví dụ, deploy sqs-consumer-economy :

```
cd services/sqs-consumer-economy
serverless deploy --stage dev
```

![1783406146804](image/_index.vi/1783406146804.png)

<div align="center"><i>Hình 5.6.5: Deploy Consumer sqs thành công.</i></div>

#### 5.6.4 Test SQS FIFO

##### * Xác nhận Producer Lambda gửi được message vào SQS FIFO

![1783409513213](image/_index.vi/1783409513213.png)

<div align="center"><i>Hình 5.6.6: Gửi yêu cầu nhận tiền.</i></div>

![1783409553035](image/_index.vi/1783409553035.png)

<div align="center"><i>Hình 5.6.7: message được trả về.</i></div>

##### * Kiểm tra Message vào Queue

![1783409759694](image/_index.vi/1783409759694.png)

<div align="center"><i>Hình 5.6.8: NumberOfMessagesSent tăng lên khi nhận request.</i></div>

##### * Kiểm tra Consumer

![1783410182104](image/_index.vi/1783410182104.png)

<div align="center"><i>Hình 5.6.9: Consumer đã nhận được message.</i></div>

##### * FIFO Ordering

Thực hiện gửi 5 yêu cầu nhận tiền liên tiếp :

```
TOKEN="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ2YW5xdWFuMSIsImFjY291bnRJZCI6IjI2MDcwNzAwMTEiLCJyb2xlIjoiUGxheWVyIiwiZXhwIjoxNzgzNDk3NDQ0LCJpYXQiOjE3ODM0MTEwNDQsImF1ZCI6InlvdXJfYXVkaWVuY2UiLCJpc3MiOiJ5b3VyX2lzc3VlciJ9.Zz4osySEb79SBN3HI0WnUXkSrXmI4nfDBQA3b6WAz_g"
API="https://l1fbbhusal.execute-api.ap-southeast-1.amazonaws.com"

for i in 1 2 3 4 5; do
  curl -s -X POST "$API/Economy/earn" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $TOKEN" \
    -d "{\"currencyType\":\"coin\",\"amount\":$((i * 10))}"
  echo ""
done
```

![1783411392460](image/_index.vi/1783411392460.png)

<div align="center"><i>Hình 5.6.10: SequenceNumber nhỏ nhất.</i></div>

![1783411453862](image/_index.vi/1783411453862.png)

<div align="center"><i>Hình 5.6.11: SequenceNumber lớn nhất.</i></div>

SequenceNumber tăng dần theo thứ tự xử lý từ nhỏ nhất tới lớn nhất:

Message amount=20 → 18903297315744239872

Message amount=30 → 18903297315816687872

Message amount=40 → 18903297315898607872

Message amount=50 → 18903297315972591616

#### 5.6.5 Tổng kết

Hệ thống **Amazon SQS FIFO** đã được triển khai và tích hợp thành công với  **AWS Lambda** :

* Producer gửi message thành công vào SQS FIFO.
* Lambda Consumer tự động nhận và xử lý message.
* FIFO đảm bảo thứ tự xử lý các message cùng MessageGroupId.
* Hệ thống hoạt động theo mô hình xử lý bất đồng bộ, tăng hiệu năng và khả năng mở rộng.
* Cơ chế Retry và Dead Letter Queue giúp nâng cao độ tin cậy và khả năng phục hồi khi xảy ra lỗi.

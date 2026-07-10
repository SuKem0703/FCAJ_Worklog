---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# Secure Hybrid Access to S3 using VPC Endpoints

#### Overview

**AWS PrivateLink** provides private connectivity to AWS services from VPCs and your on-premises networks, without exposing your traffic to the Public Internet.

In this lab, you will learn how to create, configure, and test VPC endpoints that enable your workloads to reach AWS services without traversing the Public Internet.

You will create two types of endpoints to access Amazon S3: a Gateway VPC endpoint, and an Interface VPC endpoint. These two types of VPC endpoints offer different benefits depending on if you are accessing Amazon S3 from the cloud or your on-premises location
+ **Gateway** - Create a gateway endpoint to send traffic to Amazon S3 or DynamoDB using private IP addresses.You route traffic from your VPC to the gateway endpoint using route tables.
+ **Interface** - Create an interface endpoint to send traffic to endpoint services that use a Network Load Balancer to distribute traffic. Traffic destined for the endpoint service is resolved using DNS.

#### Content

1. [Introduction](5.1-architecture-overview/)
2. [Infrastructure Setup and Management](5.2-management/)
3. [Database Setup and Backup](5.3-database/)
4. [Project Architecture](5.4-architecture-overview/)
5. [Amazon API Gateway Setup](5.5-API-Gateway/)
6. [Amazon SQS FIFO](5.6-sqs-fifo/)
7. [AWS DLQ & AWS CloudWatch](5.7-sqs-dlq/)
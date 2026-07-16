---
title: "Week 3 Worklog"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Set up AWS cost management and configure basic security and access control.
* Research and practice configuring networking (VPC), DNS (Route53), and management tools via CLI.
* Apply automation to resource management (auto start/stop EC2, RDS) and explore AWS's new AI service.

### Tasks to be deployed this week:

| Day | Task | Start Date | End Date | Documentation / Notes |
| --- | --- | --- | --- | --- |
| Mon | - Set up account and cost management using AWS Budgets. <br> - Configure 2 free alerts: Actual 80% and Forecasted 100% within a 10 USD budget. | 18/05/2026 | 18/05/2026 | |
| Tue | - Set up Amazon VPC. <br> - Create and manage IAM Users/Roles to obtain AWS Access Key ID and AWS Secret Access Key. | 19/05/2026 | 19/05/2026 | |
| Wed - Thu | - Research and configure AWS CLI on Ubuntu EC2 environment via IAM User. <br> - Research and attempt to deploy Route53 service. | 20/05/2026 | 21/05/2026 | Forgot to shut down Route53 and incurred a $20 charge |
| Fri | - Research AWS's AI service: AWS Bedrock. | 22/05/2026 | 22/05/2026 | |
| Sat - Sun | - Set up automated start/stop for EC2 and RDS using a combination of Lambda Functions and Amazon EventBridge. | 23/05/2026 | 24/05/2026 | |

### Week 3 Results:

* Successfully configured the AWS Budgets cost alert tool (80% and 100% thresholds for a $10 budget).
* Completed setting up the Amazon VPC network and IAM permissions, successfully obtaining the Access Key ID and Secret Access Key.
* Successfully configured and utilized AWS CLI on the Ubuntu EC2 virtual machine environment.
* Gained hands-on experience deploying Route53 (and learned a resource management lesson after a $20 charge).
* Acquired an overview of the AWS Bedrock AI service.
* Optimized costs by automating the start/stop of EC2 and RDS instances via Lambda Functions and Amazon EventBridge.
---
title: "Week 2 Worklog"
date: 2026-05-11
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Research AWS services and free modules that can be directly applied to the project.
* Deploy the actual project on an EC2 virtual machine and an RDS database.

### Tasks to be deployed this week:

| Day | Task | Start Date | End Date | Documentation |
| --- | --- | --- | --- | --- |
| Mon | - Research AWS services and free modules applicable to the project: <br>&emsp; + EC2 (t3.micro) <br>&emsp; + RDS (db.t4g.micro) <br>&emsp; + Amazon Gamelift <br>&emsp; + ElastiCache (cache.t3.micro) | 11/05/2026 | 11/05/2026 | |
| Tue - Thu | - Initialize core resources: <br>&emsp; + Create an EC2 instance (t3.micro) with Ubuntu Linux OS. <br>&emsp; + Create an RDS instance (db.t4g.micro) running MySQL. <br>&emsp; + Configure a static IP for the server using Elastic IP. | 12/05/2026 | 14/05/2026 | |
| Fri - Sat | - Configure and link resources: <br>&emsp; + Link the RDS database to the EC2 instance. <br>&emsp; + Configure inbound rules (launch-wizard-x). <br>&emsp; + Leverage remaining disk space to allocate virtual RAM (swap space). | 15/05/2026 | 16/05/2026 | |
| Sun | - Deploy the project: <br>&emsp; + Use pm2 to deploy directly on the EC2 virtual machine. <br>&emsp; + Open ports to allow external access via the public IP. | 17/05/2026 | 17/05/2026 | |

### Week 2 Results:

* Clearly understood and identified free AWS services/modules suitable for the project: EC2, RDS, Amazon Gamelift, ElastiCache.
* Successfully deployed the EC2 virtual machine (Ubuntu Linux, t3.micro) and the RDS database (MySQL, db.t4g.micro).
* Successfully configured a static IP for the server via Elastic IP.
* Completed linking the RDS database to EC2 and configured the Inbound rule (launch-wizard-x) to allow connectivity.
* Optimized the virtual machine by leveraging unused disk space as virtual RAM.
* Used pm2 to deploy the project directly on EC2 and successfully opened ports to allow access from the public IP.
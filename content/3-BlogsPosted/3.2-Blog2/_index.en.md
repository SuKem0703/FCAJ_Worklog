---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
### Amazon EKS Now Supports Control Plane Egress Through Your VPC

While exploring Amazon EKS, I came across the new Customer-Routed Control Plane Egress feature. This feature allows Kubernetes Control Plane traffic to be routed through your Amazon VPC, giving you more control and better security.

![AWS Cloud architecture diagram showing EKS Control Plane egress through VPC](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/740769954_1520636753147268_6569374290610978119_n.jpg?stp=dst-jpg_tt6&cstp=mx921x535&ctp=s921x535&_nc_cat=100&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeEOWx61b8hA-5lYmEZhNsUWtNIwVyoUDzO00jBXKhQPM4hEyspulfaaBTEAx91gOQMo0e7_7o8Dz4UHRcFbWZDv&_nc_ohc=ML7L_ZDcrM4Q7kNvwEnLSLA&_nc_oc=Adq3MoZ5E_hTO2UC1-p_vnFKYBkjtRQyLc3odd_yb5sHE9fc004NAD-WzRypuvg4qXNTgwLfjqQLWC5vSjj1ubO9&_nc_zt=23&_nc_ht=scontent.fsgn2-7.fna&_nc_gid=dFpWsQnnBiVpmAoj6RTC4g&_nc_ss=7b2a8&oh=00_AQCEW_p70XQFIbV6a_QUzd8jNbkye_D0uos5c9mvKIuTjQ&oe=6A5ADFC7)

#### 3.2.1 What is Amazon EKS?

Amazon Elastic Kubernetes Service (Amazon EKS) is a managed Kubernetes service by AWS. It makes it easier to deploy and operate Kubernetes clusters without having to manage the Control Plane yourself. EKS also integrates with many AWS services such as IAM, VPC, and CloudWatch for management and monitoring.

#### 3.2.2 What's New?

Previously, Kubernetes Control Plane traffic was handled through AWS-managed network infrastructure. With the new feature, this traffic can now go through your own Amazon VPC via Elastic Network Interfaces (ENIs). This allows administrators to apply tools like Security Groups, Route Tables, VPC Endpoints, or AWS Network Firewall for better network traffic control.

#### 3.2.3 Benefits

In my opinion, this feature brings several benefits:

* Better network traffic control.
* Enhanced system security.
* Support for audit and compliance requirements.
* Convenience when using authentication services or internal systems.

#### 3.2.4 Important Notes

When using CUSTOMER_ROUTED mode, administrators need to configure the network correctly since routing will be managed by the organization. Therefore, it's important to test thoroughly before deploying in a production environment.

#### 3.2.5 Personal Review

I think this is a quite useful update from Amazon EKS. This feature gives businesses more control over traffic management and enhanced security when deploying Kubernetes on AWS. For students exploring Cloud like myself, this is also a great opportunity to understand how AWS continuously improves its services to meet real-world user needs.

#### 3.2.6 Conclusion

Customer-Routed Control Plane Egress is a notable improvement in Amazon EKS. By allowing Control Plane traffic to be routed through your Amazon VPC, the system becomes more flexible, secure, and easier to manage. I believe this feature will be widely adopted by enterprises deploying Kubernetes on AWS in the near future.

Reference: https://aws.amazon.com/vi/blogs/containers/amazon-eks-now-supports-control-plane-egress-through-your-vpc/

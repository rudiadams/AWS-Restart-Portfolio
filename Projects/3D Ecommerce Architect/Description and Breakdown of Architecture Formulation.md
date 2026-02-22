# 3D E-Commerce Architecture Implementation

## Overview

The purpose of this project was to design a cloud architecture diagram for a next-generation 3D e-commerce web application, while also explaining the choice of each AWS service in relation to its purpose within the overall system.

**Scenario:** As part of a startup team launching a 3D e-commerce platform, users would be able to interact with 3D models of products — such as furniture, gadgets, and fashion items — before purchasing. With millions of users expected globally, the platform needed to be fast, highly available, secure, and cost-efficient. As a Cloud Practitioner, my role was to design the cloud architecture using AWS services to meet these business and technical requirements.

---

## Architecture Philosophy

Like most web applications, this service needed to be built in layers. I like to think of all services like an onion — though you're seeing the full vegetable, there was a layering growth process done in order to achieve the result.

With this e-commerce web application, that layering starts with **Storage**, then **Delivery**, **Compute**, **Databases**, and finally **Monitoring and Security**.

---

## Layer 1: Storage

**Service:** Amazon S3

All 3D models, images, videos, and static website files are uploaded and stored in Amazon S3 — including 3D product models and frontend website assets.

**Why S3?** S3 provides durable and highly scalable storage at a low, pay-as-you-use rate, meaning you are only charged for what is provisioned. Storage is also automatically scalable without requiring heavy upfront provisioning, making it an ideal foundation for a platform expecting global traffic.

---

## Layer 2: Content Delivery

**Service:** Amazon CloudFront

To ensure content is available worldwide, Amazon CloudFront sits in front of S3 as the Content Delivery Network (CDN). CloudFront caches copies of 3D assets at Global Edge Locations, so users download content from the nearest server to them.

**Why CloudFront?** This significantly reduces latency and ensures high availability — cached content can still be served even if the origin is under heavy load. While a CDN does come at an added expense, the performance boost for a 3D platform makes it a worthwhile investment.

---

## Layer 3: Compute

**Services:** AWS Lambda, Amazon EC2, Elastic Load Balancer (ELB)

A combination of AWS Lambda and Amazon EC2 handles all backend application processing.

- **Amazon EC2** provides complete control over server configurations with the option to use Auto Scaling for unforeseen traffic surges. EC2 manages complex payment logic, APIs, and core web servers.
- **AWS Lambda** executes specific tasks such as background processing and notifications, optimising costs by running only when triggered — not continuously.

Using both compute models introduces some architectural complexity, but ensures the system is both flexible and cost-effective.

To keep the compute layer stable, an **Elastic Load Balancer (ELB)** distributes incoming requests across multiple EC2 instances, preventing single points of failure and maintaining high availability despite the slight latency overhead it may introduce.

---

## Layer 4: Databases

**Services:** Amazon RDS, Amazon DynamoDB, Amazon Route 53

A connected database approach is used to meet the platform's broad technical requirements.

- **Amazon RDS** handles relational data such as transactions and account information. It supports structured data, automated backups, and Multi-AZ (Multi-Availability Zone) deployments for smooth failover.
- **Amazon DynamoDB** stores high-volume product catalogues and 3D asset data. DynamoDB's millisecond latency and automatic scaling make it ideal for performance, though it does require a cost trade-off at extremely high volumes and offers less flexibility for complex relational queries compared to RDS.
- **Amazon Route 53** handles DNS and global traffic routing, performing health checks to ensure users are only directed to healthy infrastructure. Latency-based routing is used to maximise performance for a globally distributed user base.

---

## Layer 5: Monitoring and Security

**Services:** Amazon CloudWatch, AWS Trusted Advisor

To ensure continuous optimisation across the entire architecture:

- **Amazon CloudWatch** monitors metrics and logs, triggering scaling actions and detecting failures in real time.
- **AWS Trusted Advisor** provides proactive recommendations for cost savings, security improvements, and performance enhancements.

Additional security is reinforced through **IAM-controlled access** and **encrypted data transfers** across all layers.

---

## Conclusion

This layered, onion-based architecture successfully addresses the project's core business needs:

| Requirement | Solution |
|-------------|----------|
| High availability & fault tolerance | Multi-AZ RDS, ELB, CloudFront caching |
| Scalability | Lambda serverless compute, S3 on-demand storage, EC2 Auto Scaling |
| Performance | CloudFront edge delivery, DynamoDB millisecond latency, Route 53 latency routing |
| Security | IAM access control, encrypted transfers, Trusted Advisor recommendations |
| Cost efficiency | Pay-as-you-use S3, Lambda on-demand execution, right-sized EC2 instances |

While balancing the costs of services like CloudFront and the complexity of a hybrid compute environment remain considerations, the combination of these AWS services provides a secure, globally scalable, and efficient foundation for a next-generation 3D e-commerce experience. It is important to note that these are the most cost-effective options for the project at hand — intricate enough to meet requirements, while structured to reduce costs and scale up as needed.

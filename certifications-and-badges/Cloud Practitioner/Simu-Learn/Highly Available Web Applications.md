# Highly Available Web Applications

## Overview

I designed and implemented a highly available web application architecture by leveraging Application Load Balancers and EC2 Auto Scaling. Through this SimuLearn, I gained hands-on experience evaluating different scaling strategies and analyzing how load balancing distributes traffic across distributed compute resources to ensure resilience and optimal performance.

## Services I Worked With

* **Amazon EC2 Auto Scaling** — Automatically adjusts the number of EC2 instances based on demand and health status to maintain application availability
* **Amazon Elastic Compute Cloud (EC2)** — Provides scalable computing capacity and serves as the foundation for the web application tier
* **Elastic Load Balancing (ELB)** — Distributes incoming traffic across multiple EC2 instances and performs health checks to route only to healthy targets
* **Amazon Simple Storage Service (S3)** — Stores application assets and static content with built-in redundancy and availability

## What I Demonstrated

* Designed multi-AZ architectures that maintain high availability during instance failures or regional disruptions
* Analyzed Application Load Balancer capabilities and determined appropriate use cases for path-based, host-based, and request-based routing
* Implemented auto scaling groups with scaling policies that respond dynamically to CloudWatch metrics and application demand
* Evaluated horizontal scaling strategies and compared trade-offs between scaling up (larger instances) versus scaling out (more instances)
* Configured health checks and monitoring to ensure load balancers route traffic only to healthy, operational instances
* Demonstrated understanding of how distributed systems and redundancy reduce single points of failure

<img width="881" height="618" alt="Screenshot 2026-03-07 at 16 29 54" src="https://github.com/user-attachments/assets/d279891e-a3e9-480a-9bea-bc1fe4364727" />

[Highly Available Web Applications.pdf](https://github.com/user-attachments/files/25815090/Highly.Available.Web.Applications.pdf)

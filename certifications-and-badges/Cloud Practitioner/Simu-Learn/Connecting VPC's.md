# Connecting VPCs

## Overview

I analyzed and implemented VPC peering connections to enable private network communication between isolated Virtual Private Clouds. Through this SimuLearn, I configured peering connections, managed routing rules at the subnet level, and gained a deeper understanding of how VPC peering facilitates secure multi-VPC architectures without exposing traffic to the public internet.

## Services I Worked With

* **Amazon VPC (Virtual Private Cloud)** — Provides isolated network environments with customizable subnets, route tables, and network policies that form the foundation for secure cloud infrastructure
* **Amazon Elastic Compute Cloud (EC2)** — Deployed EC2 instances across multiple VPCs to test and validate peering connectivity and inter-VPC communication

## What I Demonstrated

* Analyzed VPC peering mechanics and identified how it enables private, low-latency connectivity between VPCs without internet gateway dependencies
* Planned the implementation steps required to establish peering connections, including creating peering requests, accepting connections, and updating route tables
* Configured active peering connections between two VPCs and verified bidirectional traffic flow
* Implemented subnet-specific routing to direct traffic through peering connections based on destination CIDR blocks
* Demonstrated understanding of peering limitations, such as non-transitive routing and the requirement for non-overlapping IP address spaces
* Validated peering configurations by testing EC2-to-EC2 communication across VPC boundaries

<img width="885" height="613" alt="Screenshot 2026-03-07 at 17 11 30" src="https://github.com/user-attachments/assets/b3756308-554c-452e-84fc-2455f4d2065d" />


[Connecting VPCs.pdf](https://github.com/user-attachments/files/25815334/Connecting.VPCs.pdf)

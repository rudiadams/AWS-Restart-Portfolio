# Networking Labs

## Overview
Labs I completed exploring core AWS networking concepts — building and configuring virtual networks, managing IP addressing, and deploying web servers into custom VPC environments. All labs were completed using the AWS Management Console.

---

## Labs I Completed

| Lab | Description |
|-----|-------------|
| Internet Protocols — Static and Dynamic Addresses | Investigated a dynamic IP issue on an EC2 instance and resolved it by allocating and associating an Elastic IP |
| Build Your VPC and Launch a Web Server | Built a custom VPC with public and private subnets across two Availability Zones and launched a web server into the network |

---

## Services I Worked With

- **Amazon VPC** — created and configured an isolated virtual network with custom IP ranges, subnets, and routing
- **Internet Gateway** — attached to the VPC to enable communication between public subnets and the internet
- **NAT Gateway** — configured to allow private subnet instances to access the internet without being publicly exposed
- **Route Tables** — created and associated public and private route tables to control traffic flow across subnets
- **Security Groups** — configured as virtual firewalls to control inbound HTTP traffic to EC2 instances
- **Amazon EC2** — launched instances into the VPC to host and test web server deployments
- **Elastic IP (EIP)** — allocated and associated a static public IP address to resolve a dynamic IP issue

---

## Key Tasks I Performed

- Diagnosed and replicated a dynamic IP address issue on an EC2 instance
- Allocated an Elastic IP address and associated it to an EC2 instance to provide a persistent public IP
- Confirmed the EIP remained static across multiple stop/start cycles
- Created a VPC using the VPC Wizard with custom IPv4 CIDR blocks
- Created four subnets (two public, two private) across two Availability Zones
- Associated subnets to their appropriate public and private route tables
- Created a security group allowing inbound HTTP traffic from anywhere
- Launched an EC2 web server instance into the VPC using a User Data script
- Verified the web server was publicly accessible via the instance's Public IPv4 DNS

---

## What I Demonstrated

Through these labs, I demonstrated knowledge of:

- The difference between dynamic and static public IP addressing in AWS
- How Elastic IPs provide persistent public addressing for EC2 instances
- VPC architecture including subnets, internet gateways, NAT gateways, and route tables
- The difference between public and private subnets and how routing determines accessibility
- Security group configuration to control inbound network traffic
- Deploying and verifying a web server on an EC2 instance within a custom VPC

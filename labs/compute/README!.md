# Compute Labs

## Overview
Labs I completed exploring Amazon EC2 — AWS's core compute service. These labs focused on launching, configuring, monitoring, and managing virtual server instances in the cloud using the AWS Management Console.

---

## Labs I Completed

| Lab | Description |
|-----|-------------|
| EC2 Instance Setup | Launched a web server EC2 instance with termination protection, modified its security group, resized the instance and storage volume, and terminated it |
| Internet Protocols — Static and Dynamic Addresses | Investigated a dynamic IP issue on an EC2 instance and resolved it by allocating and associating an Elastic IP |

---

## Services I Worked With

- **Amazon EC2** — launched and managed virtual server instances in the cloud with full control over instance type, storage, networking, and security
- **Amazon EBS** — modified Elastic Block Store volumes attached to EC2 instances to increase storage capacity
- **Security Groups** — configured inbound rules to control HTTP access to EC2 instances
- **Elastic IP (EIP)** — allocated and associated a static public IP address to resolve a dynamic IP issue
- **User Data scripts** — used bootstrap scripts to automatically install and configure an Apache web server on instance launch
- **EC2 Instance Connect / Session Manager** — connected to instances directly through the AWS Management Console

---

## Key Tasks I Performed

- Launched an EC2 instance with a custom name, AMI, instance type, and VPC configuration
- Enabled termination protection to prevent accidental instance deletion
- Used a User Data script to automatically deploy an Apache web server on launch
- Monitored instance health and captured an instance screenshot via the console
- Updated a security group to allow inbound HTTP traffic
- Stopped an instance and resized it from `t3.micro` to `t3.small`
- Increased an attached EBS volume from 8 GiB to 10 GiB
- Tested and disabled termination protection before terminating the instance
- Replicated a dynamic IP issue by observing public IP changes across stop/start cycles
- Resolved the issue by allocating an Elastic IP and associating it to the instance

---

## What I Demonstrated

Through these labs, I demonstrated knowledge of:

- Launching and configuring EC2 instances following AWS best practices
- The EC2 instance lifecycle — launching, stopping, resizing, and terminating
- Security group configuration to control network access
- The difference between dynamic public IPs and static Elastic IPs
- Using User Data scripts for automated server configuration on launch
- EBS volume management and live storage resizing
- Termination protection as a safeguard against accidental deletion

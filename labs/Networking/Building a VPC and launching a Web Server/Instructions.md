# Build Your VPC and Launch a Web Server

## Overview

A Virtual Private Cloud (VPC) is the foundation of any AWS network architecture. It provides an isolated, customisable network environment where you can launch and manage AWS resources securely. Understanding how to build a VPC from scratch — including subnets, route tables, and security groups — is a core cloud practitioner skill.

In this lab, I built a fully functional VPC for a Fortune 100 customer, configured public and private subnets across two Availability Zones, set up routing and security, and launched a web server EC2 instance into the network.

---

## Topics Covered

After completing this lab, I was able to:

- Create a VPC with public and private subnets using the VPC Wizard
- Create additional subnets across a second Availability Zone
- Associate subnets to route tables and configure routing
- Create a security group to control inbound traffic
- Launch an EC2 instance into the VPC and deploy a web server

---

## Introducing the Technologies

### Amazon VPC

Amazon VPC (Virtual Private Cloud) allows you to provision a logically isolated section of the AWS cloud where you can launch resources in a network you define. You have full control over your virtual networking environment, including IP address ranges, subnets, route tables, and network gateways.

### Key VPC Concepts

| Concept | Description |
|---------|-------------|
| **VPC** | An isolated virtual network within AWS |
| **Public Subnet** | A subnet with a route to an internet gateway — resources can communicate with the internet |
| **Private Subnet** | A subnet without a direct route to the internet — resources are isolated from public access |
| **Internet Gateway** | A VPC component that enables communication between the VPC and the internet |
| **NAT Gateway** | Allows instances in private subnets to access the internet without being publicly accessible |
| **Route Table** | A set of rules that determines where network traffic is directed |
| **Security Group** | A virtual firewall that controls inbound and outbound traffic for instances |

---

## Task 1: Create the VPC

In this task, I used the VPC Wizard to create a VPC, an internet gateway, and two subnets in a single Availability Zone.

1. In the AWS Management Console, searched for and selected **VPC**.
2. Chose **Create VPC** and configured the following:

| Setting | Value |
|---------|-------|
| Resources to create | VPC and more |
| Name tag auto-generation | Unchecked |
| IPv4 CIDR | `10.0.0.0/16` |
| IPv6 CIDR block | No IPv6 CIDR block |
| Tenancy | Default |
| Number of Availability Zones | 1 |
| Number of public subnets | 1 |
| Number of private subnets | 1 |
| Public subnet CIDR | `10.0.0.0/24` |
| Private subnet CIDR | `10.0.1.0/24` |
| NAT gateways | In 1 AZ |
| VPC endpoints | None |

3. In the **Preview** pane, named the resources as follows:
   - **VPC:** `Lab VPC`
   - **Public subnet:** `Public Subnet 1`
   - **Private subnet:** `Private Subnet 1`
   - **Public route table:** `Public Route Table`
   - **Private route table:** `Private Route Table`

4. Chose **Create VPC**, then chose **View VPC** to confirm the configuration.

> ✅ **Task complete:** Successfully created Lab VPC with one public and one private subnet, an internet gateway, and a NAT gateway.

---

## Task 2: Create Additional Subnets

In this task, I created two additional subnets in a second Availability Zone to support high availability across the architecture.

### Public Subnet 2

1. In the left navigation pane, chose **Subnets** → **Create subnet**.
2. Configured the following:
   - **VPC ID:** `Lab VPC`
   - **Subnet name:** `Public Subnet 2`
   - **Availability Zone:** No preference
   - **IPv4 CIDR block:** `10.0.2.0/24`
3. Chose **Create subnet**.

### Private Subnet 2

1. Chose **Create subnet** again and configured the following:
   - **VPC ID:** `Lab VPC`
   - **Subnet name:** `Private Subnet 2`
   - **Availability Zone:** No preference
   - **IPv4 CIDR block:** `10.0.3.0/24`
2. Chose **Create subnet**.

> ✅ **Task complete:** Successfully created Public Subnet 2 and Private Subnet 2 in a second Availability Zone.

---

## Task 3: Associate Subnets to Route Tables

In this task, I associated the new subnets to their appropriate route tables to ensure traffic is routed correctly.

### Associate Public Subnet 2

1. In the left navigation pane, chose **Route Tables**.
2. Selected **Public Route Table**.
3. Chose the **Subnet associations** tab → **Edit subnet associations**.
4. Selected **Public Subnet 2** and chose **Save associations**.

### Associate Private Subnet 2

1. Selected **Private Route Table**.
2. Chose the **Subnet associations** tab → **Edit subnet associations**.
3. Selected **Private Subnet 2** and chose **Save associations**.

> ✅ **Task complete:** Successfully associated both new subnets to their respective route tables. The VPC now has public and private subnets configured across two Availability Zones.

---

## Task 4: Create a Security Group

In this task, I created a security group to act as a virtual firewall for the web server instance, allowing inbound HTTP traffic.

1. In the left navigation pane, chose **Security Groups** → **Create security group**.
2. Configured the following:
   - **Security group name:** `Web Security Group`
   - **Description:** `Enable HTTP access`
   - **VPC:** `Lab VPC`
3. Under **Inbound rules**, chose **Add rule** and configured:
   - **Type:** `HTTP`
   - **Source:** `Anywhere-IPv4`
   - **Description:** `Permit web requests`
4. Chose **Create security group**.

> ✅ **Task complete:** Successfully created the Web Security Group allowing inbound HTTP traffic from anywhere.

---

## Task 5: Launch the Web Server Instance

In this task, I launched an EC2 instance into the VPC and used a User Data script to automatically deploy a web server and application files.

1. In the AWS Management Console, searched for and selected **EC2**.
2. In the left navigation pane, chose **Instances** → **Launch Instances**.
3. Configured the instance with the following settings:

| Setting | Value |
|---------|-------|
| Name | `Web Server 1` |
| AMI | Amazon Linux 2 AMI (HVM) |
| Instance type | `t3.micro` |
| Key pair | `vockey` |
| VPC | `Lab VPC` |
| Subnet | `Public Subnet 2` |
| Auto-assign public IP | Enabled |
| Security group | `Web Security Group` |

4. Expanded **Advanced details** and entered the following User Data script:

```bash
#!/bin/bash
# Install Apache Web Server and PHP
yum install -y httpd mysql php

# Download Lab files
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/

# Turn on web server
chkconfig httpd on
service httpd start
```

5. Chose **Launch Instance** → **View all instances**.
6. Waited for **Web Server 1** to show **2/2 checks passed** in the Status check column.

### Verify the Web Server

1. Selected the **Web Server 1** instance and chose the **Details** tab.
2. Copied the **Public IPv4 DNS** value.
3. Opened a new browser tab, pasted the DNS value, and pressed **Enter**.

The web server application loaded successfully, confirming the instance and VPC configuration were working correctly.

> ✅ **Task complete:** Successfully launched a web server EC2 instance into the VPC and confirmed it was publicly accessible via the Public IPv4 DNS address.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Created a VPC with public and private subnets using the VPC Wizard
- ✅ Created additional subnets across a second Availability Zone for high availability
- ✅ Associated subnets to public and private route tables
- ✅ Created a security group to permit inbound HTTP traffic
- ✅ Launched an EC2 web server instance into the VPC and verified public access

---

## Additional Resources

- [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Subnets for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html)
- [Security Groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [AWS Training and Certification](https://aws.amazon.com/training/)

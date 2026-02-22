# EC2 Instance Setup

## Overview

Amazon EC2 is one of the most fundamental services in AWS, providing resizable compute capacity in the cloud. Knowing how to correctly launch, configure, monitor, and manage an EC2 instance is a core cloud practitioner skill.

In this lab, I launched an Amazon EC2 instance with termination protection enabled and used a User Data script to automatically deploy a simple Apache web server. I then monitored the instance, updated its security group to allow HTTP traffic, resized both the instance type and storage volume, tested termination protection, and finally terminated the instance.

---

## Topics Covered

After completing this lab, I was able to:

- Launch an EC2 instance with termination protection enabled
- Deploy a web server automatically using a User Data script
- Monitor an EC2 instance using the AWS Management Console
- Modify a security group to allow HTTP access
- Resize an EC2 instance type and EBS volume
- Test and disable termination protection
- Terminate an EC2 instance

---

## Introducing the Technologies

### Amazon EC2

Amazon EC2 (Elastic Compute Cloud) provides scalable compute capacity in the cloud. Rather than investing in physical hardware, EC2 allows you to launch virtual servers — called **instances** — on demand. Instances can be started, stopped, resized, and terminated as needed, making them highly flexible for a wide range of workloads.

### Key EC2 Concepts

| Concept | Description |
|---------|-------------|
| **AMI** | Amazon Machine Image — the template used to launch an instance (OS, software) |
| **Instance Type** | Defines the CPU and memory allocated to an instance (e.g. t3.micro, t3.small) |
| **Security Group** | Acts as a virtual firewall controlling inbound and outbound traffic |
| **EBS Volume** | Elastic Block Store — persistent storage attached to an EC2 instance |
| **User Data** | A script that runs automatically when an instance first launches |
| **Termination Protection** | A setting that prevents an instance from being accidentally terminated |

---

## Task 1: Launch the EC2 Instance

In this task, I configured and launched an EC2 instance named **Web Server** via the AWS Management Console.

1. In the AWS Management Console, searched for and selected **EC2**.
2. Chose **Instances** → **Launch Instances**.
3. Configured the following settings:
   - **Name:** `Web Server`
   - **AMI:** Amazon Linux 2023 Kernel-6.1 (free tier, pre-selected)
   - **Instance type:** `t3.micro`
   - **Key pair:** Proceeded without a key pair as it was not required

4. Under **Network settings**, configured the following:
   - **VPC:** `Lab VPC`
   - **Security group name:** `Web Server Security Group`
   - Added a description for the security group
   - Removed all default inbound security group rules

5. Left storage at the default configuration to keep costs low.

6. Expanded **Advanced details** and scrolled down to **Termination protection** → set to **Enabled**.

7. Scrolled down to the **User Data** text box and entered the following script:

```bash
#!/bin/bash
yum install -y httpd
systemctl enable httpd
systemctl start httpd
echo "<html><h1>Hello from my EC2 Web Server!</h1></html>" > /var/www/html/index.html
```

> 📝 **Note:** This script installs an Apache web server, configures it to start automatically on boot, activates it, and creates a simple web page.

8. Chose **Launch Instance**.

> ✅ **Task complete:** Successfully launched the Web Server EC2 instance. The instance passed all status checks and was confirmed as running.

---

## Task 2: Monitor the Instance

In this task, I monitored the running EC2 instance using the AWS Management Console.

1. In the EC2 dashboard, selected the **Web Server** instance.
2. Navigated to the **Monitoring** tab to review instance metrics.
3. Used **Actions** → **Monitor and troubleshoot** → **Get instance screenshot** to capture a view of the instance console.

> ✅ **Task complete:** Successfully reviewed instance monitoring data and captured an instance screenshot.

---

## Task 3: Update the Security Group to Allow HTTP Access

In this task, I updated the Web Server Security Group to allow inbound HTTP traffic so the web server could be accessed from a browser.

1. Copied the instance's **Public IPv4 address** from the instance details panel.
2. In the left navigation pane, chose **Security Groups**.
3. Selected **Web Server Security Group**.
4. Chose **Actions** → **Edit inbound rules**.
5. Added the following inbound rule:
   - **Type:** `HTTP`
   - **Source:** `Anywhere-IPv4`
6. Chose **Save rules**.

> ✅ **Task complete:** Successfully updated the security group to allow HTTP traffic on port 80.

---

## Task 4: Resize the Instance and EBS Volume

In this task, I stopped the instance and resized both the instance type and the attached EBS storage volume.

### Step 1: Stop the Instance

1. Selected the **Web Server** instance.
2. Chose **Instance state** → **Stop instance** and confirmed.
3. Waited for the instance state to show **Stopped**.

### Step 2: Change the Instance Type

1. With the instance stopped, chose **Actions** → **Instance settings** → **Change instance type**.
2. Selected `t3.small` (one tier above t3.micro).
3. Chose **Apply**.

### Step 3: Resize the EBS Volume

1. In the left navigation pane, chose **Volumes**.
2. Selected the volume attached to the Web Server instance.
3. Chose **Actions** → **Modify volume**.
4. Changed the size from `8 GiB` to `10 GiB`.
5. Chose **Modify** and confirmed.

### Step 4: Restart the Instance

1. Returned to **Instances**.
2. Selected the **Web Server** instance and chose **Instance state** → **Start instance**.

> ✅ **Task complete:** Successfully resized the instance type to t3.small and increased the EBS volume from 8 GiB to 10 GiB.

---

## Task 5: Test and Disable Termination Protection

In this task, I verified that termination protection was working correctly, then disabled it and terminated the instance.

### Step 1: Attempt to Terminate

1. Selected the **Web Server** instance.
2. Chose **Instance state** → **Terminate instance** and confirmed.

The termination was blocked with an error, confirming that termination protection was active.

### Step 2: Disable Termination Protection

1. Chose **Actions** → **Instance settings** → **Change termination protection**.
2. Unchecked the **Enable** box.
3. Chose **Save**.

### Step 3: Terminate the Instance

1. Chose **Instance state** → **Terminate instance**.
2. Confirmed the termination.

The instance moved to a **Terminated** state successfully.

> ✅ **Task complete:** Successfully tested termination protection, disabled it, and terminated the EC2 instance.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Launched an EC2 instance with a User Data script to deploy a web server
- ✅ Monitored the instance using the AWS Management Console
- ✅ Modified a security group to allow HTTP access
- ✅ Resized the instance type and EBS volume
- ✅ Tested and disabled termination protection
- ✅ Terminated the EC2 instance

---

## Additional Resources

- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [Amazon EBS Volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes.html)
- [EC2 Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)
- [Working with User Data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)
- [AWS Training and Certification](https://aws.amazon.com/training/)

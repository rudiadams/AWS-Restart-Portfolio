# Internet Protocols — Static and Dynamic Addresses

## Overview

Understanding the difference between static and dynamic IP addresses is a fundamental networking concept in AWS. When an EC2 instance is assigned a public IP address by default, that address is dynamic — meaning it changes every time the instance is stopped and restarted. This can break any resources or services that depend on a consistent IP address.

In this lab, I took on the role of a cloud support engineer responding to a customer ticket. The customer, Bob, reported that his EC2 instance was changing its public IP address every time it was stopped and started, causing his infrastructure to break. I replicated the issue, identified the root cause, and resolved it by allocating and associating an Elastic IP (EIP) to the instance.

---

## Topics Covered

After completing this lab, I was able to:

- Analyse the difference between statically and dynamically assigned IP addresses
- Replicate a dynamic IP issue on an EC2 instance
- Allocate an Elastic IP (EIP) address
- Associate an EIP to an EC2 instance to provide a persistent public IP
- Confirm the solution by stopping and restarting the instance

---

## Introducing the Technologies

### Dynamic vs Static IP Addresses

By default, when an EC2 instance is launched with a public IP address, that address is **dynamically assigned** — it is drawn from AWS's pool of available addresses and changes each time the instance is stopped and restarted. This is suitable for temporary workloads but problematic for anything requiring a consistent address.

A **static IP address** remains the same regardless of instance state changes, ensuring that dependent resources are never broken by an unexpected address change.

### Elastic IP Address (EIP)

An Elastic IP is a static, public IPv4 address provided by AWS that can be allocated to your account and associated with any EC2 instance. Unlike a standard public IP, an EIP persists independently of the instance — it does not change when the instance is stopped and restarted.

### Key Networking Concepts

| Concept | Description |
|---------|-------------|
| **Public IPv4** | Externally accessible IP address assigned to an instance |
| **Private IPv4** | Internal IP address used within the VPC — remains constant |
| **Dynamic IP** | Default public IP that changes on every stop/start cycle |
| **Elastic IP (EIP)** | A persistent, static public IP address allocated from AWS |
| **VPC** | Virtual Private Cloud — the isolated network environment hosting the instance |

---

## Task 1: Replicate the Customer's Issue

In this task, I launched a new EC2 instance to replicate the dynamic IP behaviour Bob was experiencing.

### Step 1: Launch a Test Instance

1. In the AWS Management Console, searched for and selected **EC2**.
2. In the left navigation pane, chose **Instances** → **Launch Instances**.
3. Configured the instance with the following settings:
   - **AMI:** Amazon Linux 2 AMI (HVM)
   - **Instance type:** `t3.micro`
   - **Network:** `Lab VPC`
   - **Subnet:** `Public Subnet 1`
   - **Auto-assign Public IP:** `Enabled`
   - **Tag:** Key `Name`, Value `test instance`
   - **Security group:** Selected existing group `Linux Instance SG`
   - **Key pair:** `vockey | RSA`
4. Chose **Launch Instances**.
5. Waited for the instance status to show **2/2 checks passed** before proceeding.

### Step 2: Observe the IP Address Before Stopping

1. Selected the checkbox for **test instance**.
2. Navigated to the **Networking** tab at the bottom.
3. Noted the **Public IPv4 address** and **Private IPv4 address**.

### Step 3: Stop the Instance and Observe Changes

1. Chose **Instance state** → **Stop instance**.
2. Waited for the instance state to change to **Stopped**.
3. Navigated back to the **Networking** tab and observed the IP addresses.

> 📝 **Note:** When stopped, the Public IPv4 address is released back to AWS. The Private IPv4 address remains unchanged.

### Step 4: Restart and Confirm the IP Has Changed

1. Chose **Instance state** → **Start instance**.
2. Waited for the instance state to return to **Running**.
3. Navigated to the **Networking** tab and noted the new **Public IPv4 address**.

The public IP address had changed — confirming that Bob's instance was using a **dynamic IP address**. The private IP address remained the same throughout, as expected.

> ✅ **Task complete:** Successfully replicated the customer's issue. The EC2 instance was confirmed to be using a dynamic public IP address that changes on every stop/start cycle.

---

## Task 2: Resolve the Issue Using an Elastic IP

In this task, I allocated an Elastic IP address and associated it with the test instance to provide a persistent, static public IP.

### Step 1: Allocate an Elastic IP

1. In the left navigation pane, under **Network & Security**, chose **Elastic IPs**.
2. Chose **Allocate Elastic IP address**.
3. Left all settings as default and chose **Allocate**.
4. Noted the newly allocated EIP address.

### Step 2: Associate the EIP to the Instance

1. Selected the checkbox for the newly created EIP.
2. Chose **Actions** → **Associate Elastic IP address**.
3. Configured the association as follows:
   - **Resource type:** `Instance`
   - **Instance:** `test instance`
   - **Private IP address:** Selected the private IP associated with the instance
4. Chose **Associate**.

### Step 3: Confirm the EIP is Now the Public IP

1. Navigated back to **Instances** in the left pane.
2. Selected **test instance** and opened the **Networking** tab.
3. Confirmed that the **Public IPv4 address** now matched the allocated EIP.

### Step 4: Verify the IP Persists After Stop/Start

1. Chose **Instance state** → **Stop instance** and waited for **Stopped**.
2. Chose **Instance state** → **Start instance** and waited for **Running**.
3. Navigated to the **Networking** tab and confirmed the Public IPv4 address remained the same.

The EIP address did not change — confirming the issue was resolved.

> ✅ **Task complete:** Successfully allocated and associated an Elastic IP address. The public IP address now remains static across stop/start cycles, resolving the customer's issue.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Replicated a dynamic IP issue on an EC2 instance
- ✅ Identified that a default public IP is dynamically assigned and changes on restart
- ✅ Allocated an Elastic IP address from AWS
- ✅ Associated the EIP to the EC2 instance for a persistent static public IP
- ✅ Confirmed the solution by stopping and restarting the instance

The root cause of Bob's issue was that his EC2 instance was relying on a default dynamic public IP address. By attaching an Elastic IP, the public address becomes persistent and no longer changes when the instance is stopped and restarted — keeping all dependent resources intact.

---

## Additional Resources

- [Amazon EC2 Public IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html)
- [Elastic IP Addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
- [AWS Training and Certification](https://aws.amazon.com/training/)

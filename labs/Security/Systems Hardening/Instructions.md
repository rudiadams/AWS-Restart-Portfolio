# Systems Hardening with Patch Manager via AWS Systems Manager

## Overview

In this lab, I used AWS Systems Manager Patch Manager to implement a structured patching strategy across a fleet of six EC2 instances — three running Amazon Linux 2 and three running Windows Server 2019. I patched the Linux instances using AWS-managed default patch baselines, then created a custom Windows patch baseline targeting critical and important security updates. I used EC2 instance tags to organise instances into patch groups, executed patching operations using the **Patch now** feature, and verified full compliance across all instances through the Patch Manager dashboard.

---

## Topics Covered

After completing this lab, I was able to:

- Use AWS Systems Manager Fleet Manager to review managed EC2 instances
- Patch Linux instances using the AWS default patch baseline via instance tags
- Create a custom patch baseline for Windows Server targeting security updates
- Apply patch group tags to Windows EC2 instances
- Patch Windows instances using a custom baseline and the Patch now feature
- Monitor patching progress through the AWS-PatchNowAssociation execution status
- Verify patch compliance for all instances using the Patch Manager dashboard and compliance reporting tab

---

## Introducing the Technologies

### AWS Systems Manager (SSM)

AWS Systems Manager is a management service that provides operational visibility and control over AWS infrastructure. It enables administrators to automate common operational tasks, manage configurations, and maintain security compliance across EC2 instances at scale — without requiring direct SSH or RDP access.

### Patch Manager

Patch Manager is a capability of AWS Systems Manager that automates the process of patching managed instances with both security-related and other types of updates. It supports patching for a wide range of operating systems and integrates with Run Command to execute patching operations on demand or on a schedule via maintenance windows.

### Fleet Manager

Fleet Manager is a Systems Manager capability that provides a unified interface for managing EC2 instances. It displays node details including OS type, platform, and the associated IAM role that grants SSM access.

### SSM Documents

SSM documents define the actions that Systems Manager performs on managed instances. Patch Manager uses the `RunPatchBaseline` SSM document behind the scenes when executing patching operations via Run Command.

### Key Concepts

| Term | Definition |
|---|---|
| **Patch Baseline** | A set of rules that defines which patches are approved or rejected for a given OS, including classification, severity, and auto-approval delay |
| **Default Patch Baseline** | AWS-managed baselines provided for each supported OS — used as-is without customisation |
| **Custom Patch Baseline** | A user-defined baseline offering granular control over patch classifications, severity filters, and auto-approval timelines |
| **Patch Group** | A logical grouping of instances defined by an EC2 tag (`Patch Group`) that associates instances with a specific patch baseline |
| **Auto-Approval** | The number of days after a patch is released before it is automatically approved for installation |
| **Compliance Reporting** | A Patch Manager view showing each instance's patch compliance status, noncompliant counts, last operation date, and baseline ID |
| **Patching Operation** | The mode in which Patch Manager runs — either **Scan** (assess only) or **Scan and Install** (assess and apply) |
| **Run Command** | An SSM capability used by Patch Manager to execute the `RunPatchBaseline` document on target instances |
| **IAM Instance Role** | An IAM role attached to each EC2 instance that grants it permission to communicate with Systems Manager |

---

## Tasks

### Task 1: Patch Linux Instances Using the Default Baseline

I navigated to **AWS Systems Manager** using the console search bar, then chose **Fleet Manager** under Node Management in the left navigation pane.

📝 **Note:** The six EC2 instances — three Linux and three Windows — were pre-existing resources configured as part of the lab environment. Each instance has an IAM role attached that grants Systems Manager access, which is why they appear in Fleet Manager.

I selected **Linux-1** and chose **View details** from the **Node actions** dropdown to review its platform type, OS name, and associated IAM role.

I then returned to the Systems Manager homepage and navigated to **Patch Manager → Patch now** to initiate patching on the Linux instances.

I configured the patching operation as follows:

| Setting | Value |
|---|---|
| Patching operation | Scan and install |
| Reboot option | Reboot if needed |
| Instances to patch | Patch only the target instances I specify |
| Target selection | Specify instance tags |
| Tag key | Patch Group |
| Tag value | LinuxProd |

I chose **Add**, then **Patch now** to initiate the operation.

📝 **Note:** The `LinuxProd` tag was a pre-existing configuration applied to the Linux instances during lab setup — no manual tagging was required for this step.

In the **AWS-PatchNowAssociation** panel, I monitored the **Status** field and the **Scan/Install operation summary** until all three Linux instances completed successfully.

✅ **Task complete.** Successfully patched all three Linux instances using the `AWS-AmazonLinux2DefaultPatchBaseline`.

---

### Task 2: Create a Custom Patch Baseline for Windows Instances

I navigated to **Patch Manager** and chose the **Patch baselines** tab, then selected **Create patch baseline**.

#### Patch Baseline Details

| Setting | Value |
|---|---|
| Name | WindowsServerSecurityUpdates |
| Description | Windows security baseline patch |
| Operating system | Windows |
| Set as default patch baseline | *(left unchecked)* |

#### Approval Rules

I configured two approval rules under **Approval rules for operating systems**:

**Rule 1 — Critical Security Updates**

| Setting | Value |
|---|---|
| Products | WindowsServer2019 |
| Severity | Critical |
| Classification | SecurityUpdates |
| Auto-approval | 3 days |
| Compliance reporting | Critical |

**Rule 2 — Important Security Updates**

| Setting | Value |
|---|---|
| Products | WindowsServer2019 |
| Severity | Important |
| Classification | SecurityUpdates |
| Auto-approval | 3 days |
| Compliance reporting | High |

I chose **Create patch baseline**.

#### Associate the Baseline with a Patch Group

In the **Patch baselines** list, I selected the **WindowsServerSecurityUpdates** baseline, opened the **Actions** dropdown, and chose **Modify patch groups**.

I entered `WindowsProd` in the **Patch groups** field, chose **Add**, then **Close**.

📝 **Note:** This association means any EC2 instance tagged with `Patch Group: WindowsProd` will automatically use this custom baseline when patched.

✅ **Task complete.** Successfully created the `WindowsServerSecurityUpdates` custom patch baseline and associated it with the `WindowsProd` patch group.

---

### Task 3: Patch Windows Instances

#### Task 3.1: Tag Windows Instances

I navigated to **EC2 → Instances** and selected **Windows-1**. In the **Tags** tab, I chose **Manage tags → Add new tag** and configured the following:

| Key | Value |
|---|---|
| Patch Group | WindowsProd |

I chose **Save**, then repeated this process for **Windows-2** and **Windows-3**.

💭 **Consider:** The `Patch Group` tag key is a reserved key that SSM recognises natively. By tagging instances with this key, Patch Manager automatically routes them to the patch baseline associated with the matching patch group name.

✅ **Task complete.** Successfully tagged all three Windows instances with `Patch Group: WindowsProd`.

#### Task 3.2: Patch Windows Instances

I returned to **Systems Manager → Patch Manager** and chose **Patch now**, configuring the operation as follows:

| Setting | Value |
|---|---|
| Patching operation | Scan and install |
| Reboot option | Reboot if needed |
| Instances to patch | Patch only the target instances I specify |
| Target selection | Specify instance tags |
| Tag key | Patch Group |
| Tag value | WindowsProd |

I chose **Add**, then **Patch now**.

In the resulting page, I selected the **Execution ID** link, which opened the execution record in **State Manager**. I then chose the **Output** link for an instance showing a status of **InProgress** to open the Run Command output in detail.

Expanding the **Output** panel confirmed that Patch Manager was executing the `RunPatchBaseline` document and that the `PatchGroup: WindowsProd` association was correctly applied.

📝 **Note:** Behind the scenes, Patch Manager uses Run Command to call the `RunPatchBaseline` SSM document on each target instance. The document evaluates which patches apply based on the instance's OS and associated patch baseline.

✅ **Task complete.** Successfully initiated and monitored the patching operation for all three Windows instances.

---

### Task 4: Verify Patch Compliance

I navigated to **Patch Manager → Dashboard**. Under **Compliance summary**, I confirmed:

- **Compliant: 6** — all six instances (three Linux, three Windows) were fully compliant.

I then chose the **Compliance reporting** tab to review per-instance details in the **Node patching details** panel.

For each instance, I verified the following columns:

| Column | Description |
|---|---|
| Critical noncompliant count | Number of critical patches not yet applied |
| Security noncompliant count | Number of security patches not yet applied |
| Other noncompliant count | Number of other patch types not yet applied |
| Last operation date | Timestamp of the most recent patch operation |
| Baseline ID | The patch baseline applied to this instance |

I selected the **Node ID** for one of the Windows instances and navigated to its **Patch** tab to review the specific patches that were applied, along with their **Installed Time** timestamps.

✅ **Task complete.** Successfully verified patch compliance across all six instances — all showing a Compliant status with zero noncompliant counts.

---

## Conclusion

In this lab, I successfully:

- Used Fleet Manager to review the managed EC2 instance fleet and confirm SSM connectivity
- Patched three Amazon Linux 2 instances using the `AWS-AmazonLinux2DefaultPatchBaseline` via `Patch Group: LinuxProd` tags
- Created a custom patch baseline (`WindowsServerSecurityUpdates`) targeting Critical and Important security updates for Windows Server 2019 with a 3-day auto-approval window
- Associated the custom baseline with the `WindowsProd` patch group
- Tagged three Windows Server instances with `Patch Group: WindowsProd` and executed a Scan and Install patching operation
- Monitored patch execution through the State Manager and Run Command output
- Verified full patch compliance across all six instances using the Patch Manager dashboard and compliance reporting tab

---

## Additional Resources

- [AWS Systems Manager Patch Manager Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html)
- [Working with Predefined and Custom Patch Baselines](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-baselines.html)
- [Patch Groups in Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-patchgroups.html)
- [AWS Systems Manager Fleet Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/fleet.html)
- [RunPatchBaseline SSM Document Reference](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-about-aws-runpatchbaseline.html)
- [Viewing Patch Compliance Information](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-compliance-about.html)

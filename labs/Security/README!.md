# Systems Labs

## Overview

These labs focused on systems security and hardening across AWS workloads using automated tooling available within the AWS ecosystem. I worked with Amazon Inspector for continuous vulnerability detection and AWS Systems Manager Patch Manager to enforce patch compliance — implementing the kind of proactive security practices used in production environments at scale.

---

## Labs I Completed

| Lab | Description |
|---|---|
| Using Amazon Inspector for Vulnerability Assessment and Remediation | Activated Amazon Inspector, analysed CVE findings against the National Vulnerability Database, and remediated a vulnerable Python package dependency in an AWS Lambda function |
| Systems Hardening with Patch Manager via AWS Systems Manager | Created a custom Windows patch baseline, organised EC2 instances into patch groups using tags, patched Linux and Windows fleets, and verified full compliance across all instances |

---

## Services & Tools I Worked With

- **Amazon Inspector** — automated vulnerability scanning service used to continuously assess Lambda functions for known CVEs and package-level security risks
- **AWS Systems Manager (SSM)** — centralised management platform used to operate, patch, and maintain EC2 instances at scale without direct server access
- **Patch Manager** — SSM capability used to define patch baselines, target instances via patch groups, and execute scan-and-install patching operations
- **Fleet Manager** — SSM capability used to review managed EC2 instance details including OS type, platform, and IAM role associations
- **Run Command** — SSM capability that Patch Manager uses behind the scenes to execute the `RunPatchBaseline` document on target instances
- **AWS Lambda** — serverless compute service hosting the vulnerable function scanned and remediated during the Inspector lab
- **Amazon EC2** — virtual machines running Amazon Linux 2 and Windows Server 2019, targeted for patching across both labs
- **National Vulnerability Database (NVD)** — NIST-maintained CVE reference used to interpret Inspector findings and identify remediation steps

---

## Key Tasks I Performed

- Activated Amazon Inspector and monitored Lambda function scan coverage to 100%
- Reviewed and interpreted CVE findings including severity, impacted resource, and remediation guidance
- Remediated CVE-2023-32681 by removing a pinned vulnerable version of the `requests` package in `requirements.txt` and redeploying the Lambda function
- Confirmed vulnerability remediation by verifying the finding moved to **Closed** status in Inspector
- Reviewed managed EC2 instances across a six-node fleet using Fleet Manager
- Created a custom patch baseline (`WindowsServerSecurityUpdates`) targeting Critical and Important security updates for Windows Server 2019 with a 3-day auto-approval window
- Applied `Patch Group` tags to Windows EC2 instances to associate them with the custom baseline
- Executed Scan and Install patching operations against both Linux and Windows fleets using instance tag targeting
- Monitored patching execution through State Manager and Run Command output
- Verified full patch compliance across all six instances using the Patch Manager dashboard and compliance reporting tab

---

## What I Demonstrated

- Ability to implement automated vulnerability management using Amazon Inspector across serverless workloads
- Understanding of CVE severity classification and how to cross-reference findings with the National Vulnerability Database
- Competency in remediating real-world package vulnerabilities in Lambda function dependencies
- Ability to design and enforce a structured patching strategy across a mixed OS fleet using AWS Systems Manager
- Understanding of how patch baselines, patch groups, and EC2 tags work together to route instances to the correct baseline
- Proficiency in monitoring and validating patch compliance at both the fleet and individual node level

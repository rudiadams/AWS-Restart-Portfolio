# Using Amazon Inspector for Vulnerability Assessment and Remediation

## Overview

In this lab, I used Amazon Inspector to perform automated vulnerability scanning on AWS Lambda functions. I activated the Inspector service, reviewed its findings against the National Vulnerability Database (NVD), and remediated a real CVE by updating a vulnerable Python package dependency. This lab reflects the workflow the development team at AnyCompany follows to continuously monitor and secure Lambda functions throughout the application development lifecycle.

---

## Topics Covered

After completing this lab, I was able to:

- Activate Amazon Inspector for an AWS account
- Interpret vulnerability findings and understand their severity and impact
- Cross-reference CVE findings with the National Vulnerability Database (NVD)
- Remediate package vulnerabilities in a Lambda function's dependency file
- Confirm successful remediation by reviewing closed findings in Amazon Inspector

---

## Introducing the Technologies

### Amazon Inspector

Amazon Inspector is an automated vulnerability management service that continuously scans AWS workloads for software vulnerabilities and unintended network exposure. It supports scanning of EC2 instances, Amazon ECR container images, and AWS Lambda functions — including both the function code and its associated package dependencies.

Inspector integrates with the National Vulnerability Database (NVD) to surface known CVEs, assign severity scores, and provide remediation guidance directly in the console.

### AWS Lambda

AWS Lambda is a serverless compute service that runs code in response to events without requiring server management. Lambda functions can include external Python package dependencies defined in a `requirements.txt` file. When no version is pinned, Lambda installs the latest available version of the package at deployment time.

### Key Concepts

| Term | Definition |
|---|---|
| **CVE** | Common Vulnerabilities and Exposures — a standardised identifier for publicly known security vulnerabilities |
| **NVD** | National Vulnerability Database — a NIST-maintained repository of CVE details, severity scores, and remediation guidance |
| **CVSS Score** | Common Vulnerability Scoring System — a numerical score (0–10) representing vulnerability severity |
| **Severity** | Inspector classifies findings as Critical, High, Medium, Low, or Informational |
| **Finding** | A detected vulnerability associated with a specific resource and CVE |
| **Remediation** | The action taken to resolve a vulnerability — in this context, upgrading a vulnerable package |
| **requirements.txt** | A Python dependency file that specifies which packages (and optionally which versions) a Lambda function requires |
| **Lambda Standard Scanning** | Inspector's mode that scans Lambda function code and package dependencies for known CVEs |

---

## Tasks

### Task 1: Activate Amazon Inspector

I navigated to **Amazon Inspector** using the AWS Management Console search bar.

In the left navigation panel, I chose **Activate Inspector**, then clicked the **Activate Inspector** button to enable the service for my account.

📝 **Note:** Inspector only needs to be activated once per account. After activation, it continuously scans supported resources without manual intervention.

After activation, a confirmation banner appeared: *Welcome to Inspector. Your first scan is underway.*

I dismissed the feedback survey and any banner messages, then periodically refreshed the page until the **Dashboard → Summary → Environment Coverage → Lambda functions** metric reached **100%**.

By default, Inspector enables scanning for:
- Amazon EC2 instances
- Amazon ECR container images
- AWS Lambda functions (standard scanning)

✅ **Task complete.** Successfully activated Amazon Inspector and confirmed Lambda function coverage at 100%.

---

### Task 2: Review Inspected Resources

#### Task 2.1: Review Lambda Function Findings

While waiting for the initial scan to complete, I navigated to **Findings → All Findings** in the left panel to review the results.

The findings dashboard displayed three rows — one for each detected vulnerability — with the following key columns:

| Column | Description |
|---|---|
| **Severity** | The risk level of the finding (e.g., Medium) |
| **Impacted Resource** | The Lambda function containing the vulnerability |
| **Title** | The CVE identifier and affected package |

I selected the radio button for the finding **CVE-2023-32681 - requests** to open its detail pane.

In the **Vulnerability Details** section, I chose the external link next to the Vulnerability ID to open the CVE record in the National Vulnerability Database. This page provided additional context, including the CVSS score, affected versions, and a description of the vulnerability.

In the **Remediation** section of the findings pane, Inspector confirmed that the `requests` package was outdated and recommended upgrading to a patched version.

✅ **Task complete.** Successfully reviewed Lambda function findings and identified CVE-2023-32681 in the `requests` package as the vulnerability to remediate.

---

### Task 3: Remediate Vulnerability Findings

#### Task 3.1: Update the Lambda Function's Package Dependency

I navigated to **Lambda** using the AWS Management Console search bar, then selected the **get-request** function from the list.

In the Lambda function's inline code editor, I opened `requirements.txt` in the file browser.

The file contained the following pinned dependency:

```
requests==2.20.0
```

I removed the version pin so the line read:

```
requests
```

By removing the version constraint, Lambda will install the latest available version of the `requests` package on the next deployment — ensuring the vulnerable version is no longer used.

I clicked the **Deploy** button to deploy the updated function.

A confirmation banner appeared: *Successfully updated the function get-request.*

📝 **Note:** Deploying a new version of a Lambda function automatically triggers Amazon Inspector to initiate a fresh scan of that function.

✅ **Task complete.** Successfully updated `requirements.txt` and deployed the remediated Lambda function.

---

#### Task 3.2: Confirm Remediation in Amazon Inspector

I navigated back to **Amazon Inspector** and opened **Findings → All Findings** in the left panel.

In the findings dashboard, I changed the **Finding Status** filter from **Active** to **Closed**.

The closed findings list displayed **CVE-2023-32681 - requests**, confirming that Inspector recognised the updated deployment and marked the vulnerability as resolved.

📝 **Note:** It may take a few minutes for the new scan to complete. Use the refresh button to check for updated finding statuses.

I then navigated to **Resources Coverage → Lambda Functions** and confirmed that the `get-request` function displayed an updated **Last Scanned** timestamp, verifying that Inspector had re-scanned the function post-deployment.

✅ **Task complete.** Successfully confirmed remediation — CVE-2023-32681 is now closed in Amazon Inspector.

---

## Conclusion

In this lab, I successfully:

- Activated Amazon Inspector and enabled continuous scanning for AWS Lambda functions
- Reviewed vulnerability findings and interpreted CVE details using the National Vulnerability Database
- Identified CVE-2023-32681 in the `requests` package of the `get-request` Lambda function
- Remediated the vulnerability by removing the version pin in `requirements.txt` and redeploying the function
- Confirmed successful remediation by verifying the finding moved to **Closed** status in Amazon Inspector

---

## Additional Resources

- [Amazon Inspector Documentation](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)
- [National Vulnerability Database (NVD)](https://nvd.nist.gov/)
- [CVE-2023-32681 Detail – NVD](https://nvd.nist.gov/vuln/detail/CVE-2023-32681)
- [AWS Lambda – Managing Dependencies with requirements.txt](https://docs.aws.amazon.com/lambda/latest/dg/python-package.html)
- [Amazon Inspector Findings](https://docs.aws.amazon.com/inspector/latest/user/findings-understanding.html)

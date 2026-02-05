 
AHKU Cafe – Amazon S3 Static Website Hosting Guide
Project Overview
This document describes the steps followed to host the AHKU Cafe static website using Amazon S3 Static Website Hosting as part of the AWS re/Start Portfolio Project.
Amazon S3 was selected as the hosting solution because it is cost-effective, highly available, scalable, and does not require server management—making it ideal for a small café business.
 
Prerequisites
Before starting, ensure you have:
•	An active AWS Account
•	A completed static website (HTML/CSS files)
•	The main website file named index.html
 
Step 1: Log in to the AWS Management Console
1.	Open a browser and go to https://aws.amazon.com
2.	Click Sign in to the Console
3.	Log in using your AWS account credentials
 
Step 2: Access Amazon S3
1.	In the AWS Console search bar, type S3
2.	Select Amazon S3
3.	You will be redirected to the S3 dashboard

<img width="147" height="94" alt="image" src="https://github.com/user-attachments/assets/a13ea5e5-130e-4809-85f5-97cdf59e6ceb" />
 
Step 3: Create an S3 Bucket
1.	Click Create bucket

<img width="202" height="129" alt="image" src="https://github.com/user-attachments/assets/bfc8b85c-ecf3-47f4-8498-1144c6d03fc1" />

2.	Enter a globally unique bucket name (bucket name: Ahku-cafe-website)
3.	Select a Region ( Africa (Cape Town)
4.	Leave Object Ownership as default (ACLs disabled) 

<img width="259" height="124" alt="image" src="https://github.com/user-attachments/assets/ed7437c2-1bd7-417d-95df-8f2f88147b2c" />
 
Step 4: Configure Public Access Settings
1.	Under Block Public Access settings, uncheck:
    o	✅ Block all public access
2.	Acknowledge the warning by ticking the confirmation checkbox
3.	Leave Bucket Versioning disabled
4.	Leave Default Encryption enabled(SSE-S3 enabled)

<img width="315" height="106" alt="image" src="https://github.com/user-attachments/assets/072bca55-3e64-4aee-9747-7e3382d79b6b" />

5.	Click Create bucket

<img width="382" height="58" alt="image" src="https://github.com/user-attachments/assets/ceb56529-ddba-45b6-a4cf-7472135bd0e0" />
<img width="329" height="133" alt="image" src="https://github.com/user-attachments/assets/57e0fdcf-eddb-4597-81a1-2d74fbddc516" />
 
Step 5: Upload Website Files
1.	Open the newly created bucket
2.	Click Upload
3.	Select Add files
4.	Upload index.html (and any additional files such as images, CSS, or JavaScript)
5.	Click Upload

<img width="336" height="70" alt="image" src="https://github.com/user-attachments/assets/ba24c5fc-eb65-4cf4-9919-ecce0d17046e" />
<img width="317" height="99" alt="image" src="https://github.com/user-attachments/assets/9b17a710-75b9-444d-80c6-a7dc9522d1e5" /><img width="213" height="85" alt="image" src="https://github.com/user-attachments/assets/0d204367-9bb5-4fb8-adf7-80f282b21008" />
<img width="275" height="102" alt="image" src="https://github.com/user-attachments/assets/602c87d2-be95-4676-a2f9-dd27ec565b83" />

 
Step 6: Enable Static Website Hosting
1.	Go to the Properties tab of the bucket

<img width="426" height="32" alt="image" src="https://github.com/user-attachments/assets/87d19c18-2ac8-4960-bfaf-f0b7c51e3a43" />

2.	Scroll to Static website hosting
3.	Click Edit
4.	Select Enable
5.	Choose Host a static website
6.	Enter:
7.	Index document: index.html

<img width="337" height="137" alt="image" src="https://github.com/user-attachments/assets/a5c00544-dfa1-433b-a144-433a847aa5dd" />

8.	Click Save changes

<img width="452" height="19" alt="image" src="https://github.com/user-attachments/assets/56b2d45f-d2a1-4126-9158-69ebd746d4d9" />
 
Step 7: Configure Bucket Policy for Public Access
1.	Go to the Permissions tab
2.	Scroll to Bucket policy
3.	Click Edit
4.	Paste the following policy (replace the bucket name if necessary):
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::ahku-cafe-website/*"
    }
  ]
}
5.	Click Save changes

<img width="416" height="122" alt="image" src="https://github.com/user-attachments/assets/1b215d42-d49f-4cc0-b49c-9afa96c20268" />
 
Step 8: Access the Live Website
1.	Navigate back to the Properties tab
2.	Scroll to Static website hosting
3.	Copy the Bucket website endpoint
4.	Paste the URL into a web browser to view the live AHKU Cafe website

<img width="451" height="86" alt="image" src="https://github.com/user-attachments/assets/7720d284-5175-4cec-883c-66b02da83a69" />
<img width="452" height="229" alt="image" src="https://github.com/user-attachments/assets/b73f5341-b47a-4b77-b4dc-8d64536ecaf0" />
 
Benefits of Hosting AHKU Cafe on Amazon S3
•	Low Cost: Pay only for storage and usage
•	High Availability: 99.99% availability
•	Scalability: Automatically handles traffic growth
•	No Server Management: AWS fully manages the infrastructure
•	Security: Supports encryption and IAM integration
 
Conclusion
By hosting the AHKU Cafe website on Amazon S3, the business gains a reliable, scalable, and affordable online presence. This solution removes the need for on-premises servers while improving accessibility and customer engagement.
 

<img width="451" height="694" alt="image" src="https://github.com/user-attachments/assets/2f282d89-361a-4bc7-8630-0a865380dc95" />

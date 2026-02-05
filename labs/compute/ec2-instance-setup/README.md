# EC2 Instance Setup Lab

## Objective
I launched an Amazon EC2 instance with termination protection enabled and used a User Data script to deploy a simple web server. This task focused on securely deploying, monitoring, and managing an EC2 instance while following AWS best practices.

## Key Concepts Covered
- Launching a web server with termination protection enabled
- Monitoring EC2 instances
- Modify the security group that the web server is using to allow HTTP access
- Resize Amazon EC2 instances to scale
- Test termination protection
- Terminating EC2 instances

## Outcome
Successfully launched and accessed an EC2 instance, demonstrating foundational cloud compute knowledge.

Step 1 - 
I accessed the AWS Management Console, selected the EC2 option.


<img width="693" height="334" alt="Screenshot 2026-01-26 at 13 44 39" src="https://github.com/user-attachments/assets/57631c37-b0db-4a80-9ed5-7bc17b405607" />


Once this was selected, I had to selected on "running instance" in order to launch a new EC2 instance".


<img width="870" height="366" alt="Screenshot 2026-01-26 at 13 51 06" src="https://github.com/user-attachments/assets/6b063aea-7cfd-4f7c-93cd-b555c56c171c" />


On the right hand side of the screen I selected "Launch Instances" so that I could create the instance I needed.

<img width="392" height="179" alt="Screenshot 2026-01-26 at 13 52 09" src="https://github.com/user-attachments/assets/1c86367b-0920-4223-8ca7-abb026588aab" />

I named the intance "Web Server".

<img width="726" height="393" alt="Screenshot 2026-01-26 at 13 53 29" src="https://github.com/user-attachments/assets/5ebfa024-b61e-43c0-9a83-454b12bf0c5c" />

As Amazon Linux 2023 Kernel-6.1 AMI was free, it was pre-selected and I opted to keep it.

<img width="764" height="476" alt="Screenshot 2026-01-26 at 13 54 23" src="https://github.com/user-attachments/assets/0f4ac030-dae5-4a67-a767-e3b91b6f1b6e" />

Though there are a multitude of instance types, the selection is always needs based and I went ahead and chose t3.micro as it met the requirements for my needs.

<img width="772" height="473" alt="Screenshot 2026-01-26 at 13 56 38" src="https://github.com/user-attachments/assets/a158b7ca-934a-4df9-844b-2caaefc33f7f" />

I proceeded without a keypair and it was not necessary.

<img width="585" height="346" alt="Screenshot 2026-01-26 at 13 57 10" src="https://github.com/user-attachments/assets/487b9965-a9de-4239-9c5f-713586043f9b" />

When it came to the VPC Settings, I selected that a VPC would be required and chose Lab VPC. I went ahead and named the security group while also adding descriptions:

<img width="777" height="518" alt="Screenshot 2026-01-26 at 13 59 52" src="https://github.com/user-attachments/assets/39ffeb6f-b353-4ba1-ba9d-79051021708b" />

I removed the Inbound Security Group Rules:

<img width="747" height="208" alt="Screenshot 2026-01-26 at 14 00 57" src="https://github.com/user-attachments/assets/a5baf12b-bad0-4cd3-8e19-afff462a469b" />

opted to keep the storage in order to save on costs:

<img width="772" height="235" alt="Screenshot 2026-01-26 at 14 02 42" src="https://github.com/user-attachments/assets/82cc7587-e884-44df-b870-dbe042bfd3b9" />

I opened the advanced details pane and scrolled down to termination protectiona end selected enabled.
<img width="511" height="588" alt="Screenshot 2026-01-26 at 14 03 47" src="https://github.com/user-attachments/assets/31ead46b-6510-49c6-9f86-e547ad8e00d0" />

I then made sure to add the following commands under the uder data textbox 

<img width="636" height="411" alt="Screenshot 2026-01-26 at 14 06 18" src="https://github.com/user-attachments/assets/b7adb175-14e7-4630-90b2-842850ebffc9" />

The script does the following:
- Install an Apache web server (httpd)
- Configure the web server to automatically start on boot
- Activate the Web server
- Create a simple web page
On the right side of the screen I selected to launch my instance.

<img width="389" height="461" alt="Screenshot 2026-01-26 at 14 08 02" src="https://github.com/user-attachments/assets/9f586f5c-deba-4638-9892-e6c2c8299040" />

My instance was running and passed all checks.

<img width="964" height="591" alt="Screenshot 2026-01-26 at 14 11 00" src="https://github.com/user-attachments/assets/3953127e-3697-4e1c-8a8c-6e1d659e2ee6" />

While monitoring my EC2 instance, empted to take a screenshot of what my instance looks like by following these instructions listed from 1-4 which should be selected in order:

<img width="959" height="509" alt="Screenshot 2026-01-26 at 14 16 28" src="https://github.com/user-attachments/assets/9f121751-0923-4f2f-be4d-dedc8dbb2838" />

Here is what my instance ended up looking like:

<img width="1100" height="586" alt="Screenshot 2026-01-26 at 14 19 36" src="https://github.com/user-attachments/assets/6b89da91-3cf0-4a8f-8875-da8f9c6dfe09" />

Now that I had a view of this, I went ahead and copied my instance public IPv4 to my clipboard:

<img width="294" height="107" alt="Screenshot 2026-01-26 at 14 20 37" src="https://github.com/user-attachments/assets/317a2611-8d64-4ad3-ab6d-6aeca76be499" />

I went ahead and moved over to "Security Groups" and selected the "Web Server Security Groups" and chose the options key and hit "EDIT INBOUND RULES"

<img width="940" height="463" alt="Screenshot 2026-01-26 at 14 23 54" src="https://github.com/user-attachments/assets/8d7ce2ea-9479-41d1-be61-2f253e9e1f15" />

I chose to set the inbound rules to HTTP and under source I chose "Anywhere IPv4" and saved the rules.

<img width="1177" height="325" alt="Screenshot 2026-01-26 at 14 26 14" src="https://github.com/user-attachments/assets/35aa6987-fb8e-488f-8a4c-3a2e45f47355" />

I decided to stop the instance so I could resize and changed the EBS volume as well.
Stopping the instance is quite simple:

<img width="748" height="240" alt="Screenshot 2026-01-26 at 14 30 20" src="https://github.com/user-attachments/assets/eec75939-b52b-4119-95aa-7921a65a75cc" />

You'll see I selected to changet he instance type by selecting "actions" then "instance settings" then "change instance type".

<img width="633" height="386" alt="Screenshot 2026-01-26 at 14 32 58" src="https://github.com/user-attachments/assets/3431b834-0523-4552-bd1c-d2a7497890b3" />

Made sure to select t3.small this time which is a little larger than a micro instance:

<img width="310" height="319" alt="Screenshot 2026-01-26 at 14 34 02" src="https://github.com/user-attachments/assets/690315ed-8578-4365-aef1-d2adbcd980db" />

changed the instance type accordingly:

<img width="264" height="57" alt="Screenshot 2026-01-26 at 14 36 00" src="https://github.com/user-attachments/assets/cef837c4-651f-4552-b0e8-487c48c0c2c9" />

on the left pane I selected "Volumes"

<img width="148" height="119" alt="Screenshot 2026-01-26 at 14 37 20" src="https://github.com/user-attachments/assets/ad085cc1-e7b6-4403-8b12-289e68115ea0" />

I chose the volume and then hit "actions" in order to modify the volume accordingly.

<img width="916" height="193" alt="Screenshot 2026-01-26 at 14 37 48" src="https://github.com/user-attachments/assets/3bd382d8-e98e-4f49-96a8-ccaea10dbffb" />

in the highlighted area, you'll see I modified the volumed from 8 to 10 and then submitted the request.

<img width="364" height="443" alt="Screenshot 2026-01-26 at 14 38 44" src="https://github.com/user-attachments/assets/dd0a7138-cf7c-45f2-85f5-e949f6aff8a5" />

After this I went ahead and started my instance again:

<img width="795" height="269" alt="Screenshot 2026-01-26 at 14 39 52" src="https://github.com/user-attachments/assets/fc92d98d-1d82-4923-8a84-c1f0c6c1c13d" />

Once all of this was completed, I wanted to make sure that my termination protection was working as it should, I attempted to terminate the instance by selecting "instance state" and then hit "terminate instance" which gave me an error message. I continued to proceed nonetheless:

<img width="768" height="410" alt="Screenshot 2026-01-26 at 14 42 00" src="https://github.com/user-attachments/assets/a2aa0c2b-5b69-43a1-9f9f-1477e69fc597" />

as you'll notice, this was not completed due to the termination protection being turned on:

<img width="967" height="238" alt="Screenshot 2026-01-26 at 14 42 29" src="https://github.com/user-attachments/assets/cab085d2-32b7-41ab-8f91-2e9f227fccee" />

I changed the instance termination rule and went ahead and terminated the instance:

<img width="551" height="304" alt="Screenshot 2026-01-26 at 14 44 31" src="https://github.com/user-attachments/assets/a204c55e-3dc0-4b76-9573-5cfd1d2d4f3f" />

I hit the "enable" box to disable the function and then proceeded to save:

<img width="637" height="416" alt="Screenshot 2026-01-26 at 14 45 26" src="https://github.com/user-attachments/assets/546b97ea-b357-42aa-b3e0-abfd92457c6f" />

Now we move forward and terminate the instance:

<img width="474" height="229" alt="Screenshot 2026-01-26 at 14 46 11" src="https://github.com/user-attachments/assets/e259e8d9-097b-44ea-b831-37dc7f022f62" />
<img width="747" height="434" alt="Screenshot 2026-01-26 at 14 46 34" src="https://github.com/user-attachments/assets/5c3361b3-80b4-4715-a6d1-b7b3ad2ab04b" />

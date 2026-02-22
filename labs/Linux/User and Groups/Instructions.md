# Managing Users and Groups in Linux

## Overview

User and group management is a fundamental skill in Linux system administration. Controlling who has access to what — and at what level — is essential for maintaining a secure and well-organised environment.

In this lab, I connected to an Amazon EC2 instance via SSH and created multiple users and groups, assigned users to their appropriate groups, and tested permissions by switching between accounts.

---

## Topics Covered

After completing this lab, I was able to:

- Create new users with a default password
- Create groups and assign the appropriate users
- Log in as different users and test permissions

---

## Introducing the Technologies

### Linux User Management

Linux is a multi-user operating system, meaning multiple accounts can exist on the same system simultaneously. Each user has a unique identity and set of permissions. User accounts are stored in `/etc/passwd` and group memberships are stored in `/etc/group`.

### Key Commands

| Command | Description |
|---------|-------------|
| `useradd` | Creates a new user account |
| `passwd` | Sets or updates a user's password |
| `groupadd` | Creates a new group |
| `usermod -a -G` | Adds a user to an existing group |
| `su` | Switches to another user account |
| `cat /etc/passwd` | Lists all user accounts on the system |
| `cat /etc/group` | Lists all groups and their members |

### Amazon EC2

In this lab, I connected to a pre-configured **t3.micro** EC2 instance (1 vCPU, 1 GiB memory) named **Command Host** to run all Linux commands directly in the terminal.

---

## Task 1: Connect to the EC2 Instance via SSH

The `labsuser.pem` key file was already available in my Downloads folder from the lab setup. I connected to the **Command Host** EC2 instance using the macOS terminal.

1. Navigated to the Downloads folder:

```bash
cd ~/Downloads
```

2. Updated the file permissions on the key:

```bash
chmod 400 labsuser.pem
```

3. Connected to the instance via SSH, replacing `<public-ip>` with the PublicIP address from the lab details panel:

```bash
ssh -i labsuser.pem ec2-user@<public-ip>
```

> ✅ **Task complete:** Successfully connected to the Command Host EC2 instance via SSH.

---

## Task 2: Create Users

In this task, I created ten user accounts, each with a default password. First, I confirmed I was in the correct working directory:

```bash
pwd
```

Expected output:

```
/home/ec2-user
```

For each user, I ran the following commands — for example, to create `arosalez`:

```bash
sudo useradd arosalez
sudo passwd arosalez
```

This was repeated for all ten users listed in the table below:

| First Name | Last Name | User ID   | Job Role             | Password      |
|------------|-----------|-----------|----------------------|---------------|
| Alejandro  | Rosalez   | arosalez  | Sales Manager        | P@ssword1234! |
| Efua       | Owusu     | eowusu    | Shipping             | P@ssword1234! |
| Jane       | Doe       | jdoe      | Shipping             | P@ssword1234! |
| Li         | Juan      | ljuan     | HR Manager           | P@ssword1234! |
| Mary       | Major     | mmajor    | Finance Manager      | P@ssword1234! |
| Mateo      | Jackson   | mjackson  | CEO                  | P@ssword1234! |
| Nikki      | Wolf      | nwolf     | Sales Representative | P@ssword1234! |
| Paulo      | Santos    | psantos   | Shipping             | P@ssword1234! |
| Sofia      | Martinez  | smartinez | HR Specialist        | P@ssword1234! |
| Saanvi     | Sarkar    | ssarkar   | Finance Specialist   | P@ssword1234! |

Once all users were created, I verified them by listing all accounts on the system:

```bash
sudo cat /etc/passwd | cut -d: -f1
```

> ✅ **Task complete:** Successfully created all ten user accounts.

---

## Task 3: Create Groups and Assign Users

In this task, I created six groups and assigned each user to their appropriate group based on their job role.

### Step 1: Create the Groups

```bash
sudo groupadd Sales
sudo groupadd HR
sudo groupadd Finance
sudo groupadd Shipping
sudo groupadd Managers
sudo groupadd CEO
```

> 📝 **Note:** Managers are a subset of personnel — not all personnel are managers. Some users belong to multiple groups to reflect this.

### Step 2: Verify the Groups

```bash
cat /etc/group
```

### Step 3: Assign Users to Groups

For each user, I ran `sudo usermod -a -G <group> <user-id>`. The full group assignments are as follows:

| Group    | Users                          |
|----------|--------------------------------|
| Sales    | arosalez, nwolf                |
| HR       | ljuan, smartinez               |
| Finance  | mmajor, ssarkar                |
| Shipping | eowusu, jdoe, psantos          |
| Managers | arosalez, ljuan, mmajor        |
| CEO      | mjackson                       |

For example, to add `arosalez` to the Sales and Managers groups:

```bash
sudo usermod -a -G Sales arosalez
sudo usermod -a -G Managers arosalez
```

I also added `ec2-user` to all groups to maintain administrative access.

### Step 4: Verify Group Memberships

```bash
sudo cat /etc/group
```

> ✅ **Task complete:** Successfully created all groups and assigned users accordingly.

---

## Task 4: Log In as a New User and Test Permissions

In this task, I switched to a newly created user account to test their permissions and observe how Linux enforces access control.

### Step 1: Switch User

```bash
su arosalez
```

When prompted, I entered the password:

```
P@ssword1234!
```

### Step 2: Attempt to Create a File

```bash
touch myFile.txt
```

Expected output:

```
Permission denied
```

### Step 3: Attempt to Use sudo

```bash
sudo touch myFile.txt
```

Expected output:

```
arosalez is not in the sudoers file
```

### Step 4: Exit Back to ec2-user

```bash
exit
```

### Step 5: Review the sudo Log

Back as `ec2-user`, I reviewed the secure log to confirm the failed sudo attempt was recorded:

```bash
sudo cat /var/log/secure
```

Expected log entry:

```
sudo: arosalez : user NOT in sudoers ; COMMAND=/bin/touch myFile.txt
```

> ✅ **Task complete:** Successfully tested user permissions and confirmed that standard users cannot execute privileged commands.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Created ten user accounts with a default password
- ✅ Created six groups and assigned users based on job role
- ✅ Logged in as a new user and tested permission restrictions
- ✅ Reviewed the system security log to verify sudo activity

---

## Additional Resources

- [Linux useradd Command](https://man7.org/linux/man-pages/man8/useradd.8.html)
- [Linux groupadd Command](https://man7.org/linux/man-pages/man8/groupadd.8.html)
- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [AWS Training and Certification](https://aws.amazon.com/training/)

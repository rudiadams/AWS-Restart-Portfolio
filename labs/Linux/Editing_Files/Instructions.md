# Editing Files in Linux

## Overview

Linux text editors are essential tools for any cloud practitioner. Being comfortable editing files directly in a terminal — without a graphical interface — is a core skill when working with EC2 instances and remote servers.

In this lab, I connected to an Amazon EC2 instance via SSH and practised editing files using two of the most widely used Linux text editors: **Vim** and **Nano**.

---

## Topics Covered

After completing this lab, I was able to:

- Use the `vimtutor` executable to learn and practise core Vim commands
- Create and edit files using Vim
- Create and edit files using Nano
- Copy content from a system log file and edit it

---

## Introducing the Technologies

### Vim

Vim is a powerful, keyboard-driven text editor available on virtually every Linux system. It operates in different **modes**, which can feel unfamiliar at first but allow for very fast editing once mastered.

| Mode | Description |
|------|-------------|
| **Normal mode** | Default mode for navigation and commands |
| **Insert mode** | Allows text to be typed; entered with `i` |
| **Command mode** | For saving, quitting, and other actions; entered with `:` |

### Nano

Nano is a simpler, beginner-friendly text editor. Unlike Vim, it does not use modes — you can start typing immediately after opening a file. Commands are displayed at the bottom of the screen and use keyboard shortcuts with `CTRL`.

### Amazon EC2

Amazon EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. In this lab, I connected to a pre-configured EC2 instance named **Command Host** (a `t3.micro` instance with 1 vCPU and 1 GiB memory) to run all Linux commands.

---

## Task 1: Connect to the EC2 Instance via SSH

In this task, I connected to the **Command Host** EC2 instance using SSH via the macOS terminal. The `labsuser.pem` key file was already available in my Downloads folder from the lab setup.

1. Opened a terminal and navigated to the Downloads folder:

```bash
cd ~/Downloads
```

2. Updated the file permissions on the key to allow SSH access:

```bash
chmod 400 labsuser.pem
```

3. Connected to the instance via SSH, replacing `<public-ip>` with the PublicIP address from the ec2 instance networking panel:

```bash
ssh -i labsuser.pem ec2-user@<public-ip>
```

> ✅ **Task complete:** Successfully connected to the Command Host EC2 instance via SSH.

---

## Task 2: Run the Vim Tutorial

In this task, I ran the built-in `vimtutor` program to practise core Vim navigation and editing commands.

Run the Vim tutorial:

```bash
vimtutor
```

> 📝 **Note:** If Vim is not installed, run the following command first:
> ```bash
> sudo yum install vim -y
> ```

Once complete, I exited the tutor:

```vim
:q!
```

> ✅ **Task complete:** Successfully completed the Vim tutorial covering lessons 1–3.

---

## Task 3: Create and Edit a File in Vim

In this task, I created a new file using Vim, added content, saved it, and then practised exiting without saving changes.

### Step 1: Create and Open the File

```bash
vim helloworld
```

### Step 2: Enter Insert Mode and Add Content

Press `i` to enter insert mode, then type:

```
Hello World!
This is my first file in Linux and I am editing it in Vim!
```

### Step 3: Save and Quit

Press `ESC` to return to normal mode, then run:

```vim
:wq
```

### Step 4: Reopen and Edit Without Saving

Reopen the file and press `i` to enter insert mode, then add a new line:

```
I learned how to create a file, edit and save them too!
```

This time, exit **without saving** to observe the difference:

```vim
:q!
```

> 📝 **Note:** Using `:q!` discards all changes made since the last save. The additional line will not be kept.

### Vim Quick Reference

| Command | Action |
|---------|--------|
| `i` | Enter insert mode |
| `ESC` | Return to normal mode |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `dd` | Delete the current line |
| `u` | Undo the last action |
| `:w` | Save without quitting |

> ✅ **Task complete:** Successfully created and edited a file using Vim, and practised both saving and discarding changes.

---

## Task 4: Create and Edit a File in Nano

In this task, I used Nano to create a new file. Unlike Vim, Nano does not require switching between modes — text can be typed immediately after opening the editor.

### Step 1: Create and Open the File

```bash
nano cloudworld
```

### Step 2: Add Content

Type the following directly into the editor:

```
We are using nano this time! We can simply start typing! No insert mode needed.
```

### Step 3: Save the File

Press `CTRL + O` to write (save) the file, then press `ENTER` to confirm the filename.

### Step 4: Exit Nano

Press `CTRL + X` to exit.

### Step 5: Reopen to Confirm

Reopen the file to verify the content was saved correctly:

```bash
nano cloudworld
```

> ✅ **Task complete:** Successfully created and edited a file using Nano, and confirmed the content was saved.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Used `vimtutor` to learn core Vim commands
- ✅ Created and edited a file using Vim
- ✅ Created and edited a file using Nano
- ✅ Practised saving and discarding changes in both editors

---

## Additional Resources

- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [Amazon Machine Images (AMI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
- [Vim Documentation](https://www.vim.org/docs.php)
- [Nano Documentation](https://www.nano-editor.org/docs.php)
- [AWS Training and Certification](https://aws.amazon.com/training/)

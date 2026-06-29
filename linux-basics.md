# Linux Command Reference

Linux is a powerful open-source operating system widely used in servers, cloud infrastructure, DevOps environments, cloud computing platforms, and embedded systems.

Most interactions with Linux systems are performed through the **Command Line Interface (CLI)** using a terminal. The CLI provides powerful utilities to manage files, processes, networks, packages, and system resources.

This document provides a **structured overview of essential Linux concepts and commonly used commands** for developers, system administrators, and DevOps engineers.

---

# Table of Contents

1. Linux Architecture
2. Linux Architecture Diagram
3. Linux File System Hierarchy
4. File and Directory Management
5. File Viewing and Editing
6. File Permissions and Ownership
7. File Searching and Text Processing
8. System Information
9. Process Management
10. Package Management
11. Networking Commands
12. Disk and Storage Management
13. Compression and Archiving
14. Shell and I/O Redirection
15. User and Group Management
16. Service Management (systemd)
17. Command Execution Diagrams
18. Repository Preview
19. Contributing
20. Miscellaneous Commands

---

# 1. Linux Architecture

### Theory

Linux follows a layered architecture that separates hardware from user applications.

```
Applications
      ↓
Shell
      ↓
Kernel
      ↓
Hardware
```

### Components

**Kernel**

The kernel is the core of the Linux operating system. It manages:

* CPU scheduling
* Memory management
* Device drivers
* File systems
* Process management

**Shell**

The shell is a command interpreter that allows users to interact with the kernel using commands.

Common shells:

* Bash
* Zsh
* Fish

Example:

```
echo "Hello Linux"
```

---

# 2. Linux Architecture Diagram

<div align="center">

Linux Kernel and System Architecture
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/1f7a4759-ec93-4a54-b4ab-0aae64de631b" />

</div>

This diagram shows how user applications communicate with hardware through the **shell and kernel layers**.

---

# 3. Linux File System Hierarchy

### Theory

Linux organizes files using a standardized directory structure known as the **Filesystem Hierarchy Standard (FHS)**.

Important directories:

| Directory | Description                     |
| --------- | ------------------------------- |
| `/`       | Root directory                  |
| `/bin`    | Essential user binaries         |
| `/etc`    | System configuration files      |
| `/home`   | User home directories           |
| `/var`    | Log files and variable data     |
| `/tmp`    | Temporary files                 |
| `/usr`    | User applications and utilities |
| `/root`   | Root user home directory        |

Example:

```
cd /home
ls
```

---

# 4. File and Directory Management

### Theory

Linux stores data in a hierarchical structure starting from the root directory `/`.

Common operations include:

* Navigating directories
* Creating files and folders
* Copying and moving files
* Deleting files

---

### Commands

| Command           | Description                  |
| ----------------- | ---------------------------- |
| `pwd`             | Display current directory    |
| `ls`              | List directory contents      |
| `ls -l`           | Detailed list                |
| `ls -a`           | Show hidden files            |
| `cd <dir>`        | Change directory             |
| `cd ..`           | Move to parent directory     |
| `mkdir <dir>`     | Create directory             |
| `mkdir -p <dir>`  | Create nested directories    |
| `rmdir <dir>`     | Remove empty directory       |
| `rm <file>`       | Remove file                  |
| `rm -r <dir>`     | Remove directory recursively |
| `rm -rf <dir>`    | Force delete directory       |
| `cp <src> <dest>` | Copy file                    |
| `cp -r <dir>`     | Copy directory               |
| `mv <src> <dest>` | Move or rename file          |
| `touch <file>`    | Create file                  |
| `stat <file>`     | Show file metadata           |

Example:

```
mkdir project
cd project
touch app.py
ls -l
```

---

# 5. File Viewing and Editing

### Theory

Linux provides utilities to inspect and modify files directly from the terminal. These tools are commonly used to analyze logs and edit configuration files.

### Commands

| Command          | Description         |
| ---------------- | ------------------- |
| `cat <file>`     | Display file        |
| `less <file>`    | Scroll through file |
| `more <file>`    | Basic file viewer   |
| `head <file>`    | First 10 lines      |
| `tail <file>`    | Last 10 lines       |
| `tail -f <file>` | Monitor logs        |
| `nano <file>`    | Simple editor       |
| `vim <file>`     | Advanced editor     |

Example:

```
tail -f system.log
```

---

# 6. File Permissions and Ownership

### Theory

Linux uses a permission system to control access to files.

Permission types:

* **Read (r)**
* **Write (w)**
* **Execute (x)**

Permission categories:

* Owner
* Group
* Others

Example:

```
-rwxr-xr--
```

### Commands

| Command    | Description             |
| ---------- | ----------------------- |
| `chmod`    | Change permissions      |
| `chmod +x` | Make executable         |
| `chown`    | Change file owner       |
| `chgrp`    | Change group            |
| `ls -l`    | View permissions        |
| `umask`    | Default permission mask |

Example

```
chmod 755 script.sh
```

---

# 7. File Searching and Text Processing

### Theory

Linux provides powerful utilities for searching files and processing text.

These commands are widely used for **log analysis, scripting, and automation**.

### Commands

| Command   | Description        |
| --------- | ------------------ |
| `find`    | Search files       |
| `grep`    | Search text        |
| `locate`  | Fast file search   |
| `which`   | Locate executable  |
| `whereis` | Locate binaries    |
| `awk`     | Pattern processing |
| `sed`     | Stream editing     |

Example

```
grep "error" server.log
```

---

# 8. System Information

| Command    | Description    |
| ---------- | -------------- |
| `uname -a` | System info    |
| `hostname` | Host name      |
| `uptime`   | System uptime  |
| `whoami`   | Current user   |
| `who`      | Logged users   |
| `id`       | User ID        |
| `lscpu`    | CPU info       |
| `free -h`  | Memory usage   |
| `df -h`    | Disk usage     |
| `du -sh`   | Directory size |

---

# 9. Process Management

### Theory

A **process** is a running instance of a program.

Linux provides commands to monitor and control processes.

### Commands

| Command   | Description             |
| --------- | ----------------------- |
| `ps`      | Show processes          |
| `ps aux`  | Detailed process list   |
| `top`     | Real-time monitoring    |
| `htop`    | Interactive monitor     |
| `kill`    | Stop process            |
| `kill -9` | Force stop              |
| `pkill`   | Kill by name            |
| `jobs`    | Show background jobs    |
| `bg`      | Resume background job   |
| `fg`      | Bring job to foreground |

---

# 10. Package Management

### Theory

Package managers install, update, and remove software.

Debian-based systems use **APT**.

### Commands

| Command          | Description         |
| ---------------- | ------------------- |
| `apt update`     | Update packages     |
| `apt upgrade`    | Upgrade system      |
| `apt install`    | Install software    |
| `apt remove`     | Remove software     |
| `apt purge`      | Remove config files |
| `apt autoremove` | Remove dependencies |
| `apt search`     | Search packages     |

---

# 11. Networking Commands

| Command         | Description       |
| --------------- | ----------------- |
| `ping`          | Test connectivity |
| `ip a`          | Show interfaces   |
| `ip route`      | Routing table     |
| `netstat -tuln` | Show ports        |
| `ss -tuln`      | Modern netstat    |
| `curl`          | Fetch web content |
| `wget`          | Download files    |
| `ssh`           | Remote login      |
| `scp`           | Secure copy       |

---

# 12. Disk and Storage Management

| Command    | Description        |
| ---------- | ------------------ |
| `lsblk`    | List disks         |
| `df -h`    | Disk usage         |
| `du -sh`   | Directory size     |
| `mount`    | Mount filesystem   |
| `umount`   | Unmount filesystem |
| `fdisk -l` | Disk partitions    |

---

# 13. Compression and Archiving

| Command     | Description         |
| ----------- | ------------------- |
| `tar -cvf`  | Create tar archive  |
| `tar -xvf`  | Extract tar         |
| `tar -czvf` | Create gzip archive |
| `tar -xzvf` | Extract gzip        |
| `zip`       | Create zip          |
| `unzip`     | Extract zip         |
| `gzip`      | Compress file       |
| `gunzip`    | Decompress file     |

---

# 14. Shell and I/O Redirection

Linux allows redirecting command output.

| Symbol | Description     |             |
| ------ | --------------- | ----------- |
| `>`    | Redirect output |             |
| `>>`   | Append output   |             |
| `      | `               | Pipe output |
| `<`    | Redirect input  |             |

Example:

```
ls > files.txt
cat log.txt | grep error
```

---

# 15. User and Group Management

| Command    | Description     |
| ---------- | --------------- |
| `adduser`  | Create user     |
| `userdel`  | Delete user     |
| `usermod`  | Modify user     |
| `groupadd` | Create group    |
| `groupdel` | Delete group    |
| `passwd`   | Change password |

---

# 16. Service Management (systemd)

Modern Linux systems use **systemd**.

| Command             | Description     |
| ------------------- | --------------- |
| `systemctl start`   | Start service   |
| `systemctl stop`    | Stop service    |
| `systemctl restart` | Restart service |
| `systemctl status`  | Check status    |
| `systemctl enable`  | Start on boot   |
| `systemctl disable` | Disable on boot |

Example

```
systemctl restart nginx
```

---

# 17. Command Execution Diagram

Linux Command Execution Flow
<p align="center">

<img width="450" height="430" alt="image" src="https://github.com/user-attachments/assets/2d9b582b-08a3-488b-8111-9a6aafd8652d" />

</p>

Command flow:

```
User Command
     ↓
Shell
     ↓
Kernel
     ↓
Hardware
```

---

# 18. Repository Preview

<div align="center">

<table>
<tr>
<td align="center">

Linux Terminal Preview

<img width="450" alt="Linux Terminal Preview" src="https://github.com/user-attachments/assets/2de36df1-b97e-46af-b2e1-deb94008dfc3"/>

</td>

<td align="center">

Linux Command Line Interface

<img width="450" alt="Linux Command Line Interface" src="https://github.com/user-attachments/assets/8d898e4b-5d78-4c59-ae27-30cb1d53508a"/>

</td>
</tr>
</table>

</div>

---

# 19. Contributing

Contributions are welcome to improve this repository.

Steps to contribute:

1. Fork the repository

2. Create a new branch

```
git checkout -b feature-update
```

3. Commit changes

```
git commit -m "Added new Linux command examples"
```

4. Push to your fork

```
git push origin feature-update
```

5. Open a Pull Request

Please ensure:

* Commands are accurate
* Formatting remains consistent
* Examples are tested

---

# 20. Miscellaneous Commands

| Command   | Description      |
| --------- | ---------------- |
| `date`    | Show date        |
| `cal`     | Show calendar    |
| `history` | Command history  |
| `clear`   | Clear terminal   |
| `echo`    | Print text       |
| `alias`   | Command shortcut |
| `man`     | Manual pages     |

Example

```
man ls
```
Add a Star⭐ if you find this Repository Helpful !!


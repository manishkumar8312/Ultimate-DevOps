# Linux OS

## Chapter 1: Linux Architecture, Kernel, Distributions & Installation
**Focus:** The "Big Picture" – how Linux works under the hood.

- **Linux Architecture:** Hardware → Kernel → Shell → User Space. Difference between User Mode and Kernel Mode.
- **The Kernel:** Core responsibilities (Process Scheduler, Memory Manager, Device Drivers, System Calls). 
- **System Calls:** The bridge between user space and kernel (`fork()`, `exec()`, `open()`, `read()`).
- **Distributions:** Debain vs RHEL vs SUSE families. Package managers (`apt` vs `yum`/`dnf` vs `zypper`). 
- **Installation & Bootloader:** Partitioning schemes (MBR vs GPT). GRUB2 configuration.
- **Interview Twist:** Explain what happens from the moment you press the power button to the login prompt (BIOS → MBR → GRUB → Kernel init → Initramfs → PID 1).

---

## Chapter 2: Filesystem Hierarchy Standard (FHS), File Management & Links
**Focus:** Navigating, managing, and understanding the Linux filesystem layout.

- **FHS Deep Dive:** Purpose of `/bin`, `/sbin`, `/etc`, `/var`, `/tmp`, `/proc`, `/dev`, `/home`, `/root`, `/usr`.
- **File Types:** Regular files, directories, character devices, block devices, sockets, pipes.
- **Path Navigation:** Absolute vs relative paths. `cd -`, `pushd`, `popd`.
- **File Operations:** `ls -lai` (inodes), `touch`, `cp`, `mv`, `rm`, `mkdir -p`, `rmdir`.
- **Links:** Hard links (same inode, can't cross FS) vs Symbolic/Soft links (pointer to path). 
- **Wildcards & Globbing:** `*`, `?`, `[]`, `{}` expansions.
- **Interview Twist:** What happens to a hard link and a soft link when you delete the original file?

---

## Chapter 3: Users, Groups, Permissions & Ownership (The Security Foundation)
**Focus:** Access control – the most tested topic in junior interviews.

- **User Management:** `/etc/passwd`, `/etc/shadow` (password hashing), `/etc/group`. 
- **Commands:** `useradd`, `usermod`, `userdel`, `groupadd`, `passwd`, `chage` (password aging).
- **Standard Permissions:** Read (4), Write (2), Execute (1) for Owner/Group/Others.
- **Commands:** `chmod` (octal and symbolic), `chown`, `chgrp`.
- **Special Permissions:** SUID (run as owner), SGID (inherit group), Sticky Bit (restrict deletion on shared dirs). Example: `/tmp` (1777) and `/usr/bin/passwd` (4755).
- **Default Permissions:** `umask` (how to calculate default 666/777 minus umask).
- **Interview Twist:** You see a file with permissions `-rwSr-xr--`. What does the capital `S` mean? (SUID is set, but execute bit is missing for owner – it's broken).

---

## Chapter 4: Core Commands, Text Processing (grep/sed/awk) & Redirection
**Focus:** The "Swiss Army Knife" tools – essential for parsing logs and data.

- **I/O Redirection:** `>` (stdout), `2>` (stderr), `&>` (both), `>>` (append), `|` (pipes).
- **Viewing Files:** `cat`, `less` (search with `/`), `head`, `tail -f` (follow logs).
- **Searching:** `grep` (basic, extended `-E`, `-i` case, `-r` recursive, `-A`/`-B` context lines).
- **Stream Editing:** `sed` – substitute (`s/old/new/g`), delete lines (`d`), print range (`-n '10,20p'`). **Crucial:** `sed -i` (in-place editing).
- **Column/Field Processing:** `awk` – pattern scanning. `awk -F':' '{print $1, $3}'`. Built-in variables (`NR`, `NF`, `$0`). Conditional logic in `awk`.
- **Utility Belt:** `cut` (extract columns), `sort -n -k` (sort numerically by column), `uniq -c` (count duplicates – must sort first!), `wc -l`.
- **Interview Twist:** Write a one-liner to find the top 5 IP addresses accessing a web server from an access log. *Answer: `awk '{print $1}' access.log | sort | uniq -c | sort -nr | head -5`*.

---

## Chapter 5: Processes, Job Control, Bash Scripting & Automation
**Focus:** Making the system work for you – scripting and scheduling.

- **Process Lifecycle:** `fork()` + `exec()` = new process. Parent-child relationships. Zombies vs Orphans.
- **Monitoring:** `ps auxf` (process tree), `top`/`htop` (real-time), `pstree`.
- **Signals:** `kill -l` (list signals). `SIGTERM` (15 – graceful), `SIGKILL` (9 – forced), `SIGHUP` (1 – reload config).
- **Job Control:** Foreground (`fg`), Background (`bg`), `&`, `jobs`, `Ctrl+Z` (suspend), `nohup` (persist after logout).
- **Bash Scripting (The Interview Core):**
  - Shebang (`#!/bin/bash`), Variables, Command substitution (`$(...)`).
  - Conditionals: `if [ -f "$file" ]`, `-z` (empty), `-eq` (numeric). Test operators.
  - Loops: `for`, `while read line`.
  - Exit codes (`$?`) and error handling (`set -e`, `set -x`).
  - Functions and arrays.
- **Scheduling:** `cron` syntax (`* * * * *`). `crontab -e`, `-l`, `-r`. `@reboot`. Anacron for non-24/7 servers.
- **Interview Twist:** Write a bash script that checks if a process is running, and if not, restarts it. (Hint: use `pgrep` or `ps aux | grep -v grep`).

---

## Chapter 6: System Initialization (systemd), Logging & Networking Basics
**Focus:** Managing services and making the server talk.

- **systemd Architecture:** PID 1 – the mother of all processes. Targets (`multi-user.target`, `graphical.target`) vs legacy runlevels.
- **Service Management:** `systemctl start/stop/restart/status/enable/disable`.
- **Unit Files:** Structure (`[Unit]`, `[Service]`, `[Install]`). Where they live (`/etc/systemd/system` vs `/lib/systemd/system`).
- **Logging (Journal & Syslog):**
  - `journalctl -u service -f` (follow service logs). 
  - Persistent vs volatile logs.
  - `/var/log/syslog`, `/var/log/auth.log`, `/var/log/kern.log`. `rsyslog` configuration.
- **Networking Commands:**
  - Interface config: `ip addr`, `ip link`, `ifconfig` (legacy).
  - Routing: `ip route`, `route -n`.
  - Ports & Sockets: `ss -tulpn` (supersedes `netstat`).
  - DNS: `/etc/resolv.conf`, `dig`, `nslookup`.
  - Connectivity: `ping`, `traceroute`, `curl -v`, `wget`.
- **Interview Twist:** A service fails to start. What do you do first? *Answer: `systemctl status service` to see the error, then `journalctl -xe -u service` for full logs.*

---

## Chapter 7: Storage, Disk Management, LVM, RAID & Filesystems
**Focus:** Managing physical and logical storage – a senior-level differentiator.

- **Disk Identification:** `lsblk`, `fdisk -l`, `blkid` (UUIDs).
- **Partitioning:** `fdisk`/`gdisk` (MBR vs GPT).
- **Filesystem Creation:** `mkfs.ext4`, `mkfs.xfs`. Inodes and blocks.
- **Mounting:** `mount` (temporary), `/etc/fstab` (permanent – fields: device, mountpoint, type, options, dump, pass).
- **Swap:** `swapon`, `swapoff`, `/etc/fstab` entry.
- **LVM (Logical Volume Manager):** 
  - Layers: PV (Physical Volume) → VG (Volume Group) → LV (Logical Volume).
  - Commands: `pvcreate`, `vgcreate`, `lvcreate`, `lvextend`, `lvreduce`, `resize2fs` (ext) or `xfs_growfs`.
- **RAID (Software):** `mdadm` – levels 0,1,5,6,10. Monitoring `/proc/mdstat`.
- **Space Checking:** `df -h` (filesystem usage), `du -sh *` (directory sizes).
- **Interview Twist:** You run `df -h` and see `/` is 90% full, but `du -sh /*` doesn't add up. Why? *Answer: Deleted files held open by running processes (`lsof | grep deleted`). Restart the process or truncate the file descriptor.*

---

## Chapter 8: SSH, Security, Performance Tuning & Advanced Troubleshooting
**Focus:** Securing the box, finding bottlenecks, and debugging production fires.

- **SSH Deep Dive:**
  - Key-based auth (`ssh-keygen -t ed25519`, `ssh-copy-id`).
  - Hardening: `/etc/ssh/sshd_config` (disable root login, disable password auth, change port).
  - Tunneling: Local forwarding (`-L`), Remote forwarding (`-R`), Dynamic SOCKS (`-D`).
  - `scp` vs `rsync` (delta transfer).
- **Security:** 
  - Firewalls: `ufw` (Debian) or `firewalld` (RHEL) / raw `iptables` (chains and rules).
  - SELinux/AppArmor: `getenforce`, `setenforce`, auditing denials.
  - `fail2ban` for brute-force protection.
- **Performance Monitoring (The "Profiling" tools):**
  - **CPU:** `mpstat -P ALL`, `top` (check `%us`, `%sy`, `%wa`, `%id`).
  - **Memory:** `free -h`, `vmstat 2` (si/so – swap in/out = bad).
  - **Disk I/O:** `iostat -x 2` (look at `%util` and `await`). `iotop`.
  - **Network:** `iftop`, `nethogs`, `sar -n DEV`.
- **Advanced Debugging:**
  - `strace -p PID` (trace system calls of a stuck process).
  - `lsof -i :port` (who's listening?).
  - `tcpdump -i eth0 -nn port 443` (packet capture – inspect with Wireshark).
  - `dmesg -T | tail -20` (kernel ring buffer – OOM killer events, hardware errors).
- **Interview Twist:** Server load is high (15.0), but `top` shows CPU idle at 90%. What's happening? *Answer: High load average but low CPU usage indicates processes are in "uninterruptible sleep" (D state) – usually a disk I/O bottleneck. Run `iostat` and `iotop` to confirm.*

---

### Bonus Module (Embedded in every chapter):
**Real-World Scenarios & Command Cheat Sheets:**
- How to recover root password (single-user mode / `init=/bin/bash`).
- How to extend a root partition online.
- How to migrate a service to a new server using `rsync`.
- How to debug a "Permission Denied" error (check ACLs: `getfacl`, SELinux contexts: `ls -Z`).

---

### How to Use This Syllabus for Interview Prep:
1. **Memorize the command syntax** for at least 3 tools per chapter.
2. **Practice one "Interview Twist" question** per chapter daily.
3. **For Senior Roles:** Spend 70% of your time on Chapters 7 and 8 – that's where they filter for experience.

This 8-chapter structure guarantees you cover every possible Linux topic asked in a technical interview, from "What is `ls`?" to "Why is my server swapping to death?"
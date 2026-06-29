# LINUX OPERATING SYSTEM

## Chapter 1: Introduction to Linux

* History and philosophy (Unix, GNU, Linus Torvalds)
* Open source licensing (GPL)
* Linux kernel vs distributions
* Major distribution families (Debian, RHEL, Arch, SUSE)
* Use cases: server, desktop, embedded, cloud, container

---

## Chapter 2: Installation and Setup

* Bare metal, virtual machine, WSL
* Partitioning basics (`/`, `/home`, swap)
* Bootable USB creation

---

## Chapter 3: Command Line Basics

* Shell (Bash, Zsh)
* Navigation: `pwd`, `ls`, `cd`
* File operations: `touch`, `cp`, `mv`, `rm`, `mkdir`, `rmdir`
* Viewing files: `cat`, `less`, `head`, `tail`
* Wildcards, history, autocompletion
* Getting help: `man`, `info`, `--help`

---

## Chapter 4: Linux Filesystem

* Filesystem Hierarchy Standard (FHS)
* Key directories: `/etc`, `/var`, `/usr`, `/home`, `/proc`, `/dev`, `/tmp`
* Absolute vs relative paths
* Hard links vs symbolic links
* Finding files: `find`, `locate`, `which`, `whereis`
* Disk usage: `du`, `df`
* Mounting: `mount`, `umount`, `/etc/fstab`

---

## Chapter 5: File Permissions and Ownership

* `ls -l` output interpretation
* User, group, others – read, write, execute
* `chmod`, `chown`, `chgrp`
* Special permissions: setuid, setgid, sticky bit
* Umask

---

## Chapter 6: Process Management

* PID, PPID, process states
* Listing: `ps`, `top`, `htop`, `pgrep`
* Signals: `kill`, `killall`, `pkill` (SIGTERM, SIGKILL)
* Foreground/background: `&`, `jobs`, `fg`, `bg`
* Priorities: `nice`, `renice`
* Monitoring: `uptime`, `vmstat`
* Zombie and orphan processes

---

## Chapter 7: Package Management

* Debian: APT (`.deb`) – `apt install`, `update`, `upgrade`, `remove`
* RHEL: DNF/YUM (`.rpm`)
* Repositories and PPAs
* Compiling from source (`./configure`, `make`, `make install`)
* Snap, Flatpak, AppImage

---

## Chapter 8: Shell Scripting (Bash)

* Shebang, variables, special variables (`$?`, `$@`, `$#`)
* Conditionals (`if`, `test`, `[ ]`)
* Loops (`for`, `while`)
* Functions, exit codes
* Debugging: `set -x`, `set -e`

---

## Chapter 9: Text Processing and Streams

* `grep`, `sed`, `awk`
* `sort`, `uniq`, `cut`, `wc`, `tr`, `diff`
* Pipes and redirections (`|`, `>`, `>>`, `2>`)
* Regular expressions (basic)

---

## Chapter 10: Networking Basics

* `ip`, `ping`, `traceroute`, `ss`
* `curl`, `wget`
* SSH: keys, `ssh-copy-id`, `scp`, `rsync`
* DNS: `dig`, `nslookup`
* Firewall: `ufw`

---

## Chapter 11: System Administration

* User/group management: `useradd`, `usermod`, `userdel`, `groupadd`, `passwd`
* `sudo` and `/etc/sudoers`
* `cron` and crontab
* `systemctl` (start, stop, enable, disable, status)
* `journalctl`, `dmesg`
* Archiving: `tar`, `gzip`, `zip`

---

## Chapter 12: Security Fundamentals

* Principle of least privilege
* Password policies, `/etc/shadow`
* File integrity: `md5sum`, `sha256sum`
* SELinux / AppArmor (basic modes)
* `gpg` encryption basics

---

## Chapter 13: Storage Management

* Partitioning: `fdisk`, `parted`, `lsblk`
* Filesystems: `mkfs.ext4`, `mkfs.xfs`
* Swap: `swapon`, `swapoff`
* LVM concepts: PV, VG, LV (`pvcreate`, `vgcreate`, `lvcreate`, `lvextend`)
* RAID levels 0,1,5,10 (conceptual)
* Disk quotas

---

## Chapter 14: Monitoring and Debugging

* System: `top`, `htop`, `free`, `vmstat`, `iostat`
* Network: `iftop`, `nethogs`
* Process debugging: `strace`, `ltrace`
* Performance: `perf`

---

## Chapter 15: Advanced Shell Environment

* Startup files: `.bashrc`, `.bash_profile`, `/etc/profile`
* Environment variables (`export`, `env`)
* Aliases and functions
* History management (`!!`, `!$`, `HISTSIZE`)
* Prompt customization (`PS1`)
* Terminal multiplexers: `screen`, `tmux`
* `nohup`, `disown`

---

## Chapter 16: Linux Internals (Conceptual)

* Boot process: BIOS → GRUB → Kernel → initramfs → systemd
* Runlevels / systemd targets
* Kernel modules (`lsmod`, `modprobe`)
* `/proc` and `/sys` filesystems
* System calls (`fork`, `exec`, `open`, `read`, `write`)
* Virtual memory, paging, swapping
* IPC: pipes, signals

---

## Chapter 17: Access Control Lists (ACLs)

* `getfacl`, `setfacl`
* Granting permissions to specific users/groups
* Default ACLs on directories

---

## Chapter 18: Core Utilities (Advanced)

* `xargs`, `tee`, `script`
* `dd`, `od`, `hexdump`, `base64`
* `date`, `timedatectl`
* Conditional execution (`&&`, `||`, `;`)

---

## Chapter 19: Linux in Cloud & DevOps

* Cloud instances (AWS EC2, DigitalOcean)
* SSH key management, security groups
* `fail2ban`
* Docker basics: container vs VM, `docker run`, `ps`, `exec`, logs, Dockerfile
* `docker-compose` (concept)

---

## Chapter 20: Important Interview Topics

* Linux vs Unix
* Hard link vs symbolic link
* Zombie vs orphan process
* `kill -9` vs `kill -15`
* `sudo` vs `su`
* `cron` vs systemd timers
* `ps aux` vs `ps -ef`
* How to check open ports (`ss -tulpn`)
* How to find large files (`find`)
* How to debug a high CPU process
* Common configuration files paths

---

## ⭐ Support

If this repository adds value to your learning, consider giving it a ⭐ to show your support.

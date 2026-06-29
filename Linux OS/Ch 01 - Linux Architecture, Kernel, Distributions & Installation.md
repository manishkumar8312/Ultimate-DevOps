# Chapter 1: Linux Architecture, Kernel, Distributions & Installation

## 1.1 Linux Architecture: The Layered Model

The Linux operating system follows a monolithic kernel architecture but is structured in distinct logical layers. Understanding this hierarchy is fundamental to diagnosing issues and comprehending how user commands translate into hardware actions.

- **Hardware Layer:** The physical components—CPU, RAM, disk controllers, network interface cards (NICs), and peripheral devices.
- **Kernel Space:** The core of the operating system. It runs in a protected memory region and has unrestricted access to hardware. Code executing here has privileged access to the CPU instruction set and memory management units.
- **User Space:** The environment where all user applications, shell instances, and system libraries (glibc) execute. Processes in user space cannot access hardware directly; they must request services from the kernel.
- **Shell & Utilities:** The interface between the user and the kernel. The shell (bash, zsh, sh) interprets user commands and invokes system calls via the GNU core utilities (ls, cp, mv).

### User Mode vs Kernel Mode

This is a critical security and stability distinction enforced by the CPU itself.

- **User Mode:** Processes run with restricted privileges. They have access only to their own allocated memory segments. If a process attempts to access memory outside its allocated space or execute a privileged instruction, the CPU generates a fault (general protection fault), and the kernel terminates the process. This prevents a crashing application from bringing down the entire system.
- **Kernel Mode:** Executes with full authority over the system. The kernel can execute any CPU instruction, access any memory address, and control all hardware peripherals. Transition from User Mode to Kernel Mode occurs exclusively through **system calls** or hardware interrupts (e.g., timer interrupts, I/O completion signals).

*Interview Note:* Interviewers frequently ask, "Why can't user processes write directly to disk?" The answer is security and stability—direct hardware access would bypass filesystem permissions and allow process corruption. The kernel acts as a gatekeeper.

---

## 1.2 The Kernel: Core Responsibilities

The Linux kernel is the heart of the OS. It is a monolithic kernel—meaning all core services run in a single address space for performance—but it supports loadable kernel modules (LKMs) for dynamic hardware support without recompilation.

The kernel is responsible for four primary subsystems:

1.  **Process Scheduler:** Implements the Completely Fair Scheduler (CFS). It determines which process runs on which CPU core and for how long. It handles process states (Running, Runnable, Blocked, Zombie, Stopped) and context switching—the act of saving the current process's state (registers, program counter) and loading the next process's state.

2.  **Memory Manager:** Oversees virtual memory, paging, and swapping. It maps virtual addresses (used by processes) to physical addresses in RAM via the Memory Management Unit (MMU). Key concepts include:
    - **Demand Paging:** Loading pages into memory only when accessed.
    - **Swap:** Moving inactive memory pages to disk (swap partition or file) to free RAM.
    - **OOM Killer:** When memory is exhausted, the Out-Of-Memory killer terminates processes based on a scoring system (`/proc/PID/oom_score`) to restore system stability.

3.  **Device Drivers:** Kernel modules that communicate with hardware controllers. Drivers implement standard interfaces (character devices, block devices, network devices) so the kernel can interact with diverse hardware uniformly. Devices appear as files in `/dev/`.

4.  **System Call Interface (SCI):** The fixed API through which user-space applications request kernel services. This is the *only* sanctioned entry point into kernel space.

---

## 1.3 System Calls: The Bridge Between User and Kernel Space

A system call is a programmatic request from a user process to the kernel for a privileged operation. The process traps into kernel mode by executing a software interrupt (e.g., `int 0x80` on x86, or `syscall` instruction on x86_64). The kernel then invokes the appropriate handler.

Essential system calls that every Linux engineer must know:

| System Call | Purpose | Typical User-Space Wrapper |
| :--- | :--- | :--- |
| `fork()` | Clones the calling process. Creates a child process with a copy of the parent's memory. Returns PID of child to parent, returns 0 to child. | Used by the shell to launch commands. |
| `exec()` | Family of calls (`execl`, `execvp`, `execve`). Replaces the current process image with a new binary. Does not return on success. | Used by shells to load binaries like `/bin/ls`. |
| `open()` | Opens a file or device and returns a file descriptor (integer). Requires path, flags (O_RDONLY, O_CREAT), and permissions. | Used by `cat`, `vim`, etc. |
| `read()` | Reads data from a file descriptor into a buffer. Returns the number of bytes read, or 0 at EOF. | Used by almost every utility that processes data. |
| `write()` | Writes data from a buffer to a file descriptor. | Used for output operations. |
| `close()` | Closes a file descriptor, releasing kernel resources. | Essential for avoiding file descriptor leaks. |
| `pipe()` | Creates a unidirectional inter-process communication (IPC) channel. Returns two file descriptors (read end, write end). | Foundational for shell pipelines (`grep foo | wc -l`). |
| `kill()` | Sends a signal to a process or process group. | The underlying call for the `kill` command. |
| `mmap()` | Maps files or devices into memory. Enables efficient file I/O and shared memory. | Used by database systems and dynamic linkers. |

*Interview Twist:* When you run `ls -l`, the shell calls `fork()` to create a child process, then `exec()` to load `/bin/ls`. Inside `ls`, it calls `open()` on the current directory (`.`), then repeatedly calls `getdents()` (a system call for reading directory entries), then `stat()` for each file to retrieve metadata, and finally `write()` to print the output to the terminal.

---

## 1.4 Linux Distributions: Families and Package Management

A Linux distribution is a curated collection of the Linux kernel, GNU tools, system libraries, package manager, and a selection of user applications. For interview purposes, you must distinguish between the major lineages.

### Debian Family (Debian, Ubuntu, Linux Mint)
- **Package Format:** `.deb` (Debian package).
- **High-Level Frontend:** `apt` (Advanced Package Tool) – resolves dependencies and downloads from repositories.
- **Low-Level Tool:** `dpkg` – installs, removes, and queries individual `.deb` packages without dependency resolution.
- **Essential Commands:**
  - `apt update` – Refreshes the package index from repositories (`/etc/apt/sources.list`).
  - `apt install <package>` – Installs a package and its dependencies.
  - `apt upgrade` – Upgrades all installed packages to latest versions.
  - `apt remove` – Removes a package but preserves configuration files.
  - `apt purge` – Removes package and its configuration files.
  - `dpkg -l` – Lists all installed packages.

### Red Hat Family (RHEL, CentOS, Fedora, Rocky Linux)
- **Package Format:** `.rpm` (Red Hat Package Manager).
- **High-Level Frontend:** `dnf` (Dandified YUM) – the successor to `yum`. Modern RHEL 8+ uses `dnf`.
- **Low-Level Tool:** `rpm` – handles individual package operations.
- **Essential Commands:**
  - `dnf check-update` – Refreshes repository metadata.
  - `dnf install <package>` – Installs with dependency resolution.
  - `dnf update` – Upgrades all packages.
  - `dnf remove <package>` – Removes a package.
  - `rpm -qa` – Lists all installed RPM packages.
  - `rpm -qi <package>` – Displays detailed information about an installed package.

### SUSE Family (openSUSE, SLES)
- **Package Format:** `.rpm` (shared with Red Hat, but with different tooling).
- **Package Manager:** `zypper` – powerful command-line interface.
- **Essential Commands:**
  - `zypper refresh` – Refreshes repositories.
  - `zypper install <package>` – Installs.
  - `zypper update` – Updates.

### Source-Based (Gentoo, Ports)
- **Package Manager:** `emerge` (Gentoo) – compiles source code locally with architecture-specific optimizations. Generally not covered in generalist interviews but indicates deep expertise.

*Interview Note:* You will be asked: "What is the difference between `apt update` and `apt upgrade`?" The correct answer: `update` synchronizes the package metadata (the list of available packages and versions) from repositories, while `upgrade` actually installs newer versions of the packages installed on your system. Running `upgrade` without `update` uses stale metadata.

---

## 1.5 Installation, Partitioning Schemes, and the Bootloader

### Partitioning Schemes: MBR vs GPT

Before installing Linux, the storage device must be partitioned.

- **MBR (Master Boot Record):**
  - Legacy standard, dating back to 1983.
  - Resides in the first 512 bytes of the disk.
  - Contains the primary bootloader code and the partition table.
  - Supports a maximum of **four primary partitions** (or three primary plus one extended holding logical partitions).
  - Partition entries use 32-bit Logical Block Address (LBA), limiting maximum addressable disk size to **2.2 TB**.
  - No built-in data integrity (no backup of partition table).

- **GPT (GUID Partition Table):**
  - Modern standard, part of the UEFI specification.
  - Uses 64-bit LBAs, supporting disks larger than 2.2 TB (up to 8 zettabytes).
  - Supports up to **128 partitions** by default (without extended partitions).
  - Stores a backup of the partition table at the end of the disk, providing redundancy.
  - Includes a protective MBR (at sector 0) to prevent legacy tools from mistakenly overwriting GPT disks.
  - Requires UEFI firmware for booting (though some BIOS systems can boot GPT with a BIOS-boot partition).

### The Bootloader: GRUB2

GRUB2 (Grand Unified Bootloader version 2) is the default bootloader for most Linux distributions.

- **Location:** The first stage is written to the Master Boot Record (MBR) or the EFI System Partition (ESP) on UEFI systems.
- **Configuration File:** `/boot/grub2/grub.cfg` (generated from templates in `/etc/default/grub` and scripts in `/etc/grub.d/`). Users typically edit `/etc/default/grub` and run `update-grub` (Debian) or `grub2-mkconfig -o /boot/grub2/grub.cfg` (RHEL).
- **Key features:**
  - Provides a menu to select between multiple kernels and operating systems.
  - Supports booting into single-user mode (rescue mode) by editing the kernel command line (e.g., adding `single` or `init=/bin/bash`).
  - Supports loading initial ramdisks (initramfs).

### The Initramfs (Initial RAM Filesystem)

The initramfs is a temporary root filesystem loaded into memory by the bootloader. It contains essential kernel modules and tools (like `modprobe` and `insmod`) required to mount the actual root filesystem. This is necessary because the root filesystem may reside on:
- A complex LVM volume.
- An encrypted partition (LUKS).
- A RAID array.
- A network-attached storage (NFS root).
- A filesystem driver not compiled directly into the kernel (e.g., ext4, xfs, btrfs).

The initramfs executes `/init`, which loads the necessary drivers, discovers storage devices, mounts the real root filesystem (typically at `/root`), and then performs a `pivot_root` to switch from the initramfs to the real root, subsequently launching PID 1 (systemd).

---

## 1.6 The Complete Boot Process: From Power-On to Login Prompt (Interview Core)

This is the single most frequently tested sequence in senior-level Linux interviews. The following is the authoritative step-by-step walkthrough.

**Step 1: Power-On Self-Test (POST) and Firmware Initialization**
Upon applying power, the CPU loads firmware (BIOS or UEFI) from non-volatile memory. The firmware executes the POST routine, which initializes hardware (CPU registers, RAM controllers, PCIe devices). The firmware then enumerates bootable devices according to the configured boot order (BIOS boot order or UEFI boot manager).

**Step 2: Bootloader Stage 1 – Loading the Primary Bootloader**
- **BIOS/MBR system:** The firmware reads the first sector (512 bytes) of the boot disk (the MBR) into memory at address `0x7C00`. The code in this sector (446 bytes) is extremely limited and does not understand filesystems; it loads the next stage (core image) from a fixed disk location, often from the gap between the MBR and the first partition (the "MBR gap").
- **UEFI/GPT system:** The firmware reads the EFI System Partition (ESP), which is a FAT32 partition with a GUID of `C12A7328-F81F-11D2-BA4B-00A0C93EC93B`. It executes the EFI application `\EFI\BOOT\BOOTX64.EFI` (or the distribution-specific path, e.g., `\EFI\ubuntu\grubx64.efi`). This application loads the full GRUB2 binary.

**Step 3: Bootloader Stage 2 – GRUB Core and Menu**
The second-stage GRUB binary loads from the boot partition (typically `/boot`). It reads its configuration file (`/boot/grub2/grub.cfg`), which contains menu entries, kernel parameters, and instructions to load the kernel and initramfs. By default, GRUB boots the default entry after a timeout (usually 5 seconds). The user may also edit kernel boot parameters at this stage.

**Step 4: Loading the Kernel and Initramfs into Memory**
GRUB loads the selected Linux kernel image (e.g., `vmlinuz-5.15.0-91-generic`) and its corresponding initramfs image (e.g., `initrd.img-5.15.0-91-generic`) into RAM. GRUB then passes control to the kernel entry point, transferring the system's execution from firmware/bootloader context into the Linux kernel.

**Step 5: Kernel Decompression and Initialization**
The kernel image is typically compressed (bzip2 or zstd). The kernel decompresses itself in place and begins the `start_kernel()` function. This routine performs:
- Architecture-specific setup (trap vectors, page tables).
- Console initialization.
- Memory management subsystem initialization (buddy allocator, slab allocator).
- Scheduler initialization.
- Interrupt and timer initialization.
- Mounting the initial root filesystem (from the initramfs).

**Step 6: Initramfs Execution – User-Space Preparation**
The kernel executes `/init` within the initramfs as PID 1. This script (usually a shell script or a small binary) loads necessary storage drivers (e.g., `nvme`, `sd_mod`, `dm-mod`, `ext4`). It then detects and activates any storage subsystems:
- LVM logical volumes (`vgchange -ay`).
- Software RAID arrays (`mdadm --assemble --scan`).
- Encrypted volumes (`cryptsetup luksOpen`).
Finally, the initramfs mounts the real root filesystem (as specified in the kernel boot parameter `root=`, e.g., `root=/dev/vg0/root`).

**Step 7: Pivot Root and Start PID 1 (systemd)**
The initramfs executes `pivot_root`, moving the real root filesystem to `/` and discarding the initramfs from the namespace. It then executes the real init system (PID 1). On modern systems, PID 1 is **systemd**. The kernel mounts `/proc`, `/sys`, and `/dev` as virtual filesystems.

**Step 8: systemd Target Initialization**
systemd reads its configuration from `/etc/systemd/system/default.target` (which is usually a symlink to `multi-user.target` or `graphical.target`). It then:
- Starts all system services defined in `/usr/lib/systemd/system/` and `/etc/systemd/system/`.
- Mounts filesystems defined in `/etc/fstab` (`local-fs.target`).
- Enables networking (`network.target`).
- Starts login managers (e.g., `getty@tty1` for virtual consoles, or `gdm`/`lightdm` for graphical).

**Step 9: Login Prompt**
Once `multi-user.target` is reached and `getty` processes are spawned on TTYs (or a display manager is started), the system presents a login prompt (`login:`). The kernel scheduler now balances user processes, interrupts are serviced, and the system is fully operational.

*Interview Follow-Up Question:* "What would happen if the initramfs fails to mount the root filesystem?" The system panics or drops to a `dracut` emergency shell (a limited shell within the initramfs), allowing an administrator to load missing drivers or repair the `root=` parameter.

---

## Practical Commands for Chapter 1

| Command | Use Case |
| :--- | :--- |
| `uname -r` | Display the currently running kernel version. |
| `uname -a` | Show all kernel details (kernel name, hostname, release, machine architecture). |
| `lsmod` | List loaded kernel modules (drivers). |
| `modinfo <module>` | Display detailed information about a specific kernel module. |
| `dmesg | grep -i "error"` | View kernel ring buffer messages, particularly hardware errors during boot. |
| `cat /etc/os-release` | Identify the distribution name, version, and ID. |
| `lsblk -f` | List all block devices with filesystem types and UUIDs. Useful for understanding partition layouts. |
| `df -h /boot` | Check available space on the boot partition (critical for kernel updates). |
| `grub2-editenv list` | View GRUB2 environment variables (e.g., saved default entry). |
| `systemd-analyze` | Analyze system boot performance (time taken by kernel and userspace). |
| `systemd-analyze blame` | List all running units ordered by initialization time. |

---

## Chapter 1 Summary for Interview Mastery

- The **kernel** operates in privileged Kernel Mode; applications run in restricted User Mode. System calls are the sole transition mechanism.
- The **four pillars** of the kernel are Process Scheduler, Memory Manager, Device Drivers, and the System Call Interface.
- Major distribution families differ primarily by package manager: `apt/dpkg` (Debian) vs `dnf/yum/rpm` (RHEL) vs `zypper/rpm` (SUSE).
- **GPT** supersedes MBR for larger disks and provides partition table redundancy. **UEFI** is required for booting from GPT, using the EFI System Partition.
- The boot sequence is sequential: Firmware (POST) → Bootloader (GRUB2) → Kernel load → Initramfs execution (load storage drivers) → Pivot root → systemd (PID 1) → Target initialization → Login prompt.
- The initramfs is *not* optional for complex storage setups; it provides the early user-space environment to assemble the root filesystem.

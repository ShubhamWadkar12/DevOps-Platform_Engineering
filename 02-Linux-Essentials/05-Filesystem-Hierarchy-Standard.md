# 📁 Filesystem Hierarchy Standard (FHS)


The **Filesystem Hierarchy Standard (FHS)** defines a standard structure for organizing files and directories in Linux and other Unix-like operating systems.

As a DevOps Engineer, you will frequently work with:

- Configuration files
- Application files
- Logs
- User data
- Temporary files
- System binaries
- Process information
- Storage and mount points

Understanding the Linux filesystem makes system administration and troubleshooting much easier.

---

# 📌 What is FHS?

**FHS (Filesystem Hierarchy Standard)** defines conventions for where different types of files and directories should be located.

The Linux filesystem starts from the root directory:

```text
/
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

The exact structure can vary between distributions. Modern Linux distributions may also use a **merged `/usr` layout**, where directories such as `/bin`, `/sbin`, and `/lib` are linked to locations under `/usr`.

---

# 📂 Important Linux Directories

## `/`

The `/` directory is the **root of the entire filesystem**.

Everything in the Linux filesystem exists below `/`.

Check it using:

```bash
ls /
```

---

## `/boot`

Contains files required during the boot process.

Common contents include:

```text
vmlinuz
initramfs
grub/
```

Check it using:

```bash
ls -lah /boot
```

---

## `/dev`

Contains device files that represent hardware and virtual devices.

Examples:

```text
/dev/sda
/dev/nvme0n1
/dev/null
/dev/zero
```

Check it using:

```bash
ls /dev
```

---

## `/etc`

Contains **system-wide configuration files**.

Examples:

```text
/etc/hosts
/etc/hostname
/etc/fstab
/etc/ssh/
```

Example:

```bash
cat /etc/hostname
```

For DevOps engineers, `/etc` is one of the most important directories because many system and application configurations are stored here.

---

## `/home`

Contains the home directories of regular users.

Example:

```text
/home/
├── user1/
└── user2/
```

A user's personal files are normally stored inside their home directory.

---

## `/root`

This is the **home directory of the root user**.

Do not confuse:

```text
/       → Root of the filesystem
/root   → Home directory of the root user
```

---

## `/bin`

Contains essential user command binaries.

Examples include:

```bash
ls
cp
mv
rm
cat
```

On many modern Linux distributions, `/bin` is part of the **merged `/usr` layout** and may be a symbolic link to `/usr/bin`.

---

## `/sbin`

Contains system administration binaries.

On modern merged-`/usr` systems, `/sbin` may be a symbolic link to:

```text
/usr/sbin
```

---

## `/lib`

Contains essential shared libraries and Kernel-related modules.

On modern merged-`/usr` systems, `/lib` may point to:

```text
/usr/lib
```

---

## `/media`

Used as a mount point for removable media.

Examples:

- USB drives
- CDs/DVDs

Desktop environments may automatically mount removable devices here.

---

## `/mnt`

Traditionally used as a temporary mount point for manually mounted filesystems.

Example:

```bash
sudo mount /dev/sdb1 /mnt
```

---

## `/opt`

Used for optional or additional application software.

Example:

```text
/opt/application/
```

Third-party applications may be installed here depending on the organization's practices.

---

## `/proc`

`/proc` is a **virtual filesystem** that provides information about:

- Running processes
- Kernel state
- CPU
- Memory
- System information

Examples:

```bash
cat /proc/cpuinfo
```

```bash
cat /proc/meminfo
```

```bash
ls /proc
```

`/proc` does not contain normal files stored permanently on disk. Its contents are provided dynamically by the Kernel.

---

## `/run`

Contains **runtime data** created since the system booted.

Examples include:

- Process IDs
- Unix sockets
- Service runtime information

Check it using:

```bash
ls /run
```

The contents are generally temporary and recreated after reboot.

---

## `/srv`

Contains data provided by services running on the system.

Example:

```text
/srv/
```

Its exact usage depends on the application and system configuration.

---

## `/sys`

`/sys` is another **virtual filesystem** that exposes information about:

- Devices
- Drivers
- Kernel objects
- Hardware relationships

Example:

```bash
ls /sys
```

It is commonly used by Linux utilities and administrators when inspecting hardware and Kernel information.

---

## `/tmp`

Used for temporary files.

Example:

```bash
touch /tmp/test.txt
```

Temporary files may be automatically removed depending on the system configuration.

Do not store important permanent data in `/tmp`.

---

## `/usr`

Contains most user-space programs, libraries, documentation, and shared data.

Important directories include:

```text
/usr/bin
/usr/sbin
/usr/lib
/usr/share
/usr/local
```

Examples:

```bash
ls /usr/bin
```

```bash
ls /usr/share
```

---

## `/usr/local`

Used for software and files installed locally by the system administrator rather than by the distribution's package manager.

Common locations:

```text
/usr/local/bin
/usr/local/sbin
/usr/local/lib
```

For example:

```text
/usr/local/bin/my-script
```

---

## `/var`

Contains **variable data** that changes while the system is running.

Examples include:

- Logs
- Caches
- Spool data
- Application state

Important directories:

```text
/var/log
/var/cache
/var/lib
```

---

# 📜 `/var/log`

Contains system and application logs.

Check it using:

```bash
ls /var/log
```

Depending on the distribution and configuration, you may find logs related to:

- Authentication
- System services
- Applications
- Kernel messages

On systems using `systemd`, logs are commonly accessed using:

```bash
journalctl
```

---

# 📊 Important Directories at a Glance

| Directory | Purpose |
|---|---|
| `/` | Root of the filesystem |
| `/boot` | Boot-related files |
| `/dev` | Device files |
| `/etc` | System configuration |
| `/home` | Regular users' home directories |
| `/root` | Root user's home directory |
| `/bin` | Essential user commands |
| `/sbin` | System administration commands |
| `/lib` | Essential libraries and Kernel modules |
| `/media` | Removable media |
| `/mnt` | Temporary/manual mount point |
| `/opt` | Optional application software |
| `/proc` | Process and Kernel information |
| `/run` | Runtime system data |
| `/srv` | Data served by system services |
| `/sys` | Device and Kernel information |
| `/tmp` | Temporary files |
| `/usr` | User-space programs and shared data |
| `/var` | Variable data such as logs and caches |

---

# 🔍 Useful Commands

### View the root directory

```bash
ls /
```

### Show the current directory

```bash
pwd
```

### List a directory with details

```bash
ls -lah /etc
```

### Check filesystem usage

```bash
df -h
```

### Check directory size

```bash
du -sh /var/log
```

### Find where a command is located

```bash
which bash
```

You can also use:

```bash
command -v bash
```

### Identify a file

```bash
file /etc/hosts
```

---

# 🌍 Real-World DevOps Example

Suppose an application running on a Linux server is not working.

A DevOps Engineer may investigate:

```text
/etc
  ↓
Configuration files

/var/log
  ↓
Application and system logs

/var/lib
  ↓
Application state/data

/opt
  ↓
Third-party application files

/tmp
  ↓
Temporary files

/proc
  ↓
Process and system information

/sys
  ↓
Hardware and Kernel information
```

Knowing the filesystem structure helps you quickly identify where to investigate.

---

# 🛠️ Hands-on Practice

Run these commands on your Linux environment:

```bash
ls /
```

```bash
ls -lah /etc
```

```bash
ls /var/log
```

```bash
ls /proc
```

```bash
ls /sys
```

```bash
df -h
```

```bash
du -sh /var/log
```

Then answer:

1. Where are system configuration files stored?
2. Where are logs commonly stored?
3. What is the difference between `/` and `/root`?
4. Why are `/proc` and `/sys` called virtual filesystems?
5. Where would you look for information about running processes?

---

# 💼 Interview Questions

- **What is FHS?**  
  FHS stands for **Filesystem Hierarchy Standard**. It defines conventions for organizing files and directories in Unix-like operating systems.

- **What is the root directory in Linux?**  
  `/` is the top-level directory of the Linux filesystem. All other directories exist below it.

- **What is the difference between `/` and `/root`?**  
  `/` is the root of the entire filesystem, while `/root` is the home directory of the root user.

- **What is the purpose of `/etc`?**  
  `/etc` contains system-wide configuration files.

- **What is `/var` used for?**  
  `/var` contains variable data such as logs, caches, spool data, and application state.

- **What is `/proc`?**  
  `/proc` is a virtual filesystem that provides information about running processes and Kernel state.

- **What is `/sys`?**  
  `/sys` is a virtual filesystem that exposes information about devices, drivers, and Kernel objects.

- **What is the purpose of `/tmp`?**  
  `/tmp` is used for temporary files and data.

- **What is stored in `/boot`?**  
  `/boot` contains files required during the boot process, such as Kernel and bootloader-related files.

- **What is the difference between `/home` and `/root`?**  
  `/home` contains the home directories of regular users, while `/root` is the home directory of the root user.

- **What is the purpose of `/usr`?**  
  `/usr` contains most user-space programs, libraries, documentation, and shared data.

- **Where would you normally look for Linux logs?**  
  `/var/log` commonly contains system and application logs, while `journalctl` is used to access systemd journal logs.

- **Why is understanding the Linux filesystem important for DevOps?**  
  DevOps engineers frequently work with configuration files, logs, application data, processes, storage, and system files. Understanding the filesystem makes administration and troubleshooting easier.

---

# 📚 Navigation

⬅️ Previous: **[04-Boot-Process.md](04-Boot-Process.md)**

➡️ Next: **[06-Terminal-Navigation.md](06-Terminal-Navigation.md)**

# 🚀 Linux Mini Projects

## 💼 Mini Project 1  Linux Administration Toolkit

Build a simple command-line toolkit that displays important Linux system information from a single script.

The toolkit should help a DevOps Engineer quickly inspect:

- Operating system
- Kernel
- Hostname
- Current user
- CPU
- Memory
- Disk usage
- Uptime
- Running processes
- IP information

---

### 📁 Project Structure

```text
linux-admin-toolkit/
├── linux-info.sh
└── README.md
```

---

### 📝 Requirements

Create:

```bash
mkdir -p ~/linux-projects/linux-admin-toolkit
cd ~/linux-projects/linux-admin-toolkit
```

Create the script:

```bash
touch linux-info.sh
```

Make it executable:

```bash
chmod +x linux-info.sh
```

---

### 🔧 Expected Information

Your script should display sections similar to:

```text
=================================
       LINUX ADMIN TOOLKIT
=================================

Hostname:
Operating System:
Kernel:
Current User:
Uptime:

CPU Information:
Memory Usage:
Disk Usage:

IP Address:
Running Processes:
=================================
```

---

### 🧠 Commands You Can Use

Operating system:

```bash
cat /etc/os-release
```

Kernel:

```bash
uname -r
```

Hostname:

```bash
hostname
```

Current user:

```bash
whoami
```

Uptime:

```bash
uptime
```

CPU:

```bash
lscpu
```

Memory:

```bash
free -h
```

Disk:

```bash
df -h
```

IP information:

```bash
ip addr
```

Running processes:

```bash
ps aux
```

---

### ⭐ Bonus

Add:

```text
CPU Load
Logged-in Users
Top 5 CPU-consuming Processes
Top 5 Memory-consuming Processes
```

Useful commands:

```bash
uptime
```

```bash
who
```

```bash
ps aux --sort=-%cpu | head -n 6
```

```bash
ps aux --sort=-%mem | head -n 6
```

---

# 💼 Mini Project 2 — System Information Script

### 🎯 Objective

Create a Bash script that generates a clean system information report.

---

### 📁 Project Structure

```text
system-info/
├── system-info.sh
└── README.md
```

---

### 📝 Requirements

The script should display:

```text
System Information
------------------

Hostname:
OS:
Kernel:
Architecture:
CPU:
Memory:
Disk:
Uptime:
Current User:
IP Address:
```

---

### 🔧 Useful Commands

Architecture:

```bash
uname -m
```

CPU:

```bash
nproc
```

Memory:

```bash
free -h
```

Disk:

```bash
df -h /
```

IP:

```bash
hostname -I
```

---

### ⭐ Bonus

Save the output to a file:

```bash
./system-info.sh > system-report.txt
```

Add a timestamp:

```text
Report Generated:
```

Use:

```bash
date
```

---

# 📁 Mini Project 3 — File Operations Automation

### 🎯 Objective

Create a Bash script that automatically organizes files into directories.

---

### 📁 Project Structure

```text
file-organizer/
├── organize.sh
├── input/
├── documents/
├── images/
├── archives/
└── other/
```

---

### 📝 Requirements

The script should:

1. Read files from `input/`.
2. Identify their extensions.
3. Move files into appropriate directories.
4. Display what was moved.

Example:

```text
input/
├── notes.txt
├── report.pdf
├── image.jpg
├── backup.zip
└── script.sh
```

After running:

```text
documents/
├── notes.txt
└── report.pdf

images/
└── image.jpg

archives/
└── backup.zip

other/
└── script.sh
```

---

### ⭐ Bonus

Add support for:

```text
.txt
.pdf
.doc
.docx
.jpg
.jpeg
.png
.zip
.tar
.gz
```

---

# 👤 Mini Project 4 — User Management Automation

### 🎯 Objective

Create a script that automates Linux user creation.

---

### 📁 Project Structure

```text
user-management/
├── create-users.sh
└── users.txt
```

---

### 📄 `users.txt`

Example:

```text
developer1
developer2
developer3
```

---

### 📝 Requirements

The script should:

1. Read usernames from `users.txt`.
2. Create users.
3. Create home directories.
4. Create a common group.
5. Add users to the group.
6. Display the created users.

Useful commands:

```bash
useradd
groupadd
usermod
id
```

---

### ⚠️ Important

User creation requires administrative privileges.

Use:

```bash
sudo
```

only where required.

Test this project on a lab environment rather than a production server.

---

# 🔐 Mini Project 5 — Permission Management

### 🎯 Objective

Create a script that prepares an application directory with appropriate ownership and permissions.

---

### 📁 Project Structure

```text
permission-manager/
├── setup-permissions.sh
└── app/
    ├── config/
    ├── logs/
    ├── scripts/
    └── data/
```

---

### 📝 Requirements

The script should:

1. Create the application structure.
2. Create an application user/group.
3. Set ownership.
4. Configure directory permissions.
5. Configure script permissions.
6. Display the final permissions.

Useful commands:

```bash
mkdir
groupadd
useradd
chown
chmod
ls -l
```

---

### 🎯 Expected Concept

```text
Application
     │
     ├── Owner
     ├── Group
     └── Permissions
```

The goal is to follow:

> **Principle of Least Privilege**

---

# ⚙️ Mini Project 6 — Process Monitoring Script

### 🎯 Objective

Create a script that monitors CPU and memory usage.

---

### 📁 Project Structure

```text
process-monitor/
├── monitor.sh
└── README.md
```

---

### 📝 Requirements

Display:

```text
Process Monitoring
------------------

CPU Usage:
Memory Usage:
Load Average:

Top CPU Processes:
Top Memory Processes:
```

Useful commands:

```bash
top
```

```bash
free -h
```

```bash
uptime
```

```bash
ps aux --sort=-%cpu | head
```

```bash
ps aux --sort=-%mem | head
```

---

### ⭐ Bonus

Allow the user to specify a process:

```bash
./monitor.sh nginx
```

Then check whether it is running.

Useful command:

```bash
pgrep -a nginx
```

---

# 🔄 Mini Project 7 — Service Health Checker

### 🎯 Objective

Create a script that checks whether important Linux services are running.

---

### 📁 Project Structure

```text
service-health-check/
├── health-check.sh
└── services.txt
```

---

### 📄 `services.txt`

Example:

```text
ssh
cron
```

The exact service names depend on the Linux distribution.

---

### 📝 Requirements

The script should:

1. Read service names.
2. Check whether each service exists.
3. Check whether it is active.
4. Display the result.

Example output:

```text
Service Health Check
--------------------

ssh     → RUNNING
cron    → RUNNING
nginx   → NOT RUNNING
```

Useful command:

```bash
systemctl is-active service-name
```

---

### ⭐ Bonus

Return a non-zero exit code if any required service is not running.

This makes the script useful in automation and CI/CD environments.

---

# 💾 Mini Project 8 — Linux Backup Automation

### 🎯 Objective

Create a Bash script that creates compressed backups of an application directory.

---

### 📁 Project Structure

```text
backup-automation/
├── backup.sh
├── data/
└── backups/
```

---

### 📝 Requirements

The script should:

1. Identify the source directory.
2. Create a timestamp.
3. Create a `.tar.gz` backup.
4. Store the backup in `backups/`.
5. Display the backup location.
6. Verify that the backup was created.

Example:

```text
backup-2026-08-10-2100.tar.gz
```

Useful commands:

```bash
date
```

```bash
tar -czf
```

```bash
ls -lh
```

---

### ⭐ Bonus

Implement backup retention.

For example:

```text
Keep the latest 5 backups.
Delete older backups.
```

---

# 📊 Mini Project 9 — Disk Usage Monitor

### 🎯 Objective

Create a script that checks filesystem usage and warns when disk usage becomes too high.

---

### 📁 Project Structure

```text
disk-monitor/
├── disk-monitor.sh
└── README.md
```

---

### 📝 Requirements

The script should:

1. Check disk usage.
2. Extract the usage percentage.
3. Compare it with a threshold.
4. Display a warning when the threshold is exceeded.

Example:

```text
Disk Usage Monitor
------------------

Filesystem: /
Usage: 72%

Status: OK
```

If usage is high:

```text
Filesystem: /
Usage: 92%

Status: WARNING
Disk usage is above threshold!
```

Useful command:

```bash
df -h /
```

---

### ⭐ Bonus

Allow the threshold to be passed as an argument:

```bash
./disk-monitor.sh 80
```

---

# 📝 Mini Project 10 — Log Analyzer

### 🎯 Objective

Create a script that analyzes application logs.

---

### 📁 Project Structure

```text
log-analyzer/
├── analyze.sh
├── application.log
└── README.md
```

---

### 📝 Example Log

```text
INFO Application started
INFO Database connected
ERROR Database connection failed
WARNING High memory usage
ERROR API request failed
INFO Application restarted
```

---

### Requirements

The script should count:

```text
INFO
WARNING
ERROR
```

Example output:

```text
Log Analysis
-------------

INFO:     3
WARNING:  1
ERROR:    2
```

Useful command:

```bash
grep
```

Count matches:

```bash
grep -c "ERROR" application.log
```

---

### ⭐ Bonus

Display the latest errors:

```bash
grep "ERROR" application.log | tail
```

---

# 🚀 Final Mini Project — Linux Administration Toolkit

## 🎯 Objective

Combine everything learned in Linux Fundamentals into one practical DevOps project.

Build a command-line administration toolkit capable of performing common server checks and administration tasks.

---

# 📁 Project Structure

```text
linux-administration-toolkit/
├── linux-toolkit.sh
├── modules/
│   ├── system.sh
│   ├── storage.sh
│   ├── processes.sh
│   ├── services.sh
│   └── users.sh
├── logs/
├── backups/
└── README.md
```

---

# 🧩 Required Features

Your toolkit should provide commands for:

```text
System Information
Storage Information
Process Monitoring
Service Health
User Information
Disk Usage
Log Analysis
Backup
```

---

# 🖥️ Example Interface

Your script can provide a menu:

```text
========================================
       LINUX ADMINISTRATION TOOLKIT
========================================

1. System Information
2. Storage Information
3. Process Monitoring
4. Service Health
5. User Information
6. Disk Usage
7. Log Analysis
8. Backup
9. Exit

Enter your choice:
```

---

# 1️⃣ System Information

Display:

```text
Hostname
OS
Kernel
Architecture
CPU
Memory
Uptime
Current User
IP Address
```

---

# 2️⃣ Storage Information

Display:

```text
Block Devices
Filesystems
Disk Usage
Inode Usage
Mount Points
```

Useful commands:

```bash
lsblk
```

```bash
df -h
```

```bash
df -i
```

```bash
findmnt
```

---

# 3️⃣ Process Monitoring

Display:

```text
CPU Usage
Memory Usage
Load Average
Top CPU Processes
Top Memory Processes
```

---

# 4️⃣ Service Health

Allow the user to enter a service:

```text
Enter service name:
```

Then display:

```text
Service:
Status:
```

Use:

```bash
systemctl is-active
```

---

# 5️⃣ User Information

Display:

```text
Current User
UID
GID
Groups
Home Directory
Shell
```

Useful commands:

```bash
whoami
```

```bash
id
```

```bash
echo $HOME
```

```bash
echo $SHELL
```

---

# 6️⃣ Disk Usage

Display:

```text
Filesystem
Total
Used
Available
Usage %
```

Use:

```bash
df -h
```

---

# 7️⃣ Log Analysis

Allow the user to provide a log file.

Analyze:

```text
INFO
WARNING
ERROR
```

Display counts.

---

# 8️⃣ Backup

Allow the user to specify a directory.

Create:

```text
backup-YYYY-MM-DD-HHMM.tar.gz
```

Store it in:

```text
backups/
```

---

# ⭐ Advanced Features

After completing the basic version, add:

- Command-line arguments
- Logging
- Error handling
- Input validation
- Configuration file
- Backup retention
- Service monitoring
- Disk threshold alerts
- CPU threshold alerts
- Memory threshold alerts
- Colored terminal output
- Help menu

---

# 📈 Project Development Path

Build the toolkit incrementally:

```text
Version 1
   ↓
System Information
   ↓
Version 2
   ↓
Storage Monitoring
   ↓
Version 3
   ↓
Process Monitoring
   ↓
Version 4
   ↓
Service Monitoring
   ↓
Version 5
   ↓
User Management
   ↓
Version 6
   ↓
Log Analysis
   ↓
Version 7
   ↓
Backup Automation
   ↓
Version 8
   ↓
Complete Linux Administration Toolkit
```

---

# 🧠 Skills Demonstrated

By completing these projects, you will practice:

```text
Linux Commands
      ↓
File Management
      ↓
Users & Groups
      ↓
Permissions
      ↓
Processes
      ↓
Services
      ↓
Storage
      ↓
Package Management
      ↓
Shell
      ↓
Bash Automation
```

These are foundational skills for:

- DevOps
- Cloud Engineering
- SRE
- Platform Engineering
- Linux Administration

---

# 📦 GitHub Project Structure

For your DevOps repository, you can organize the projects like:

```text
02-Linux-Essentials/
│
├── 01-Introduction-to-Linux.md
├── 02-Linux-Architecture.md
├── 03-Linux-Distributions.md
├── 04-Boot-Process.md
├── 05-Filesystem-Hierarchy-Standard.md
├── 06-Terminal-Navigation.md
├── 07-Essential-Linux-Commands.md
├── 08-Help-Commands.md
├── 09-File-Management.md
├── 10-Users-and-Groups.md
├── 11-Permissions.md
├── 12-Processes-and-Services.md
├── 13-Storage.md
├── 14-Package-Management.md
├── 15-Shell.md
├── 16-Hands-on-Labs.md
└── 17-Mini-Projects.md
```

Project source code can be stored separately:

```text
projects/
└── linux/
    ├── linux-admin-toolkit/
    ├── system-info/
    ├── file-organizer/
    ├── user-management/
    ├── permission-manager/
    ├── process-monitor/
    ├── service-health-check/
    ├── backup-automation/
    ├── disk-monitor/
    └── log-analyzer/
```

---

# 💼 Interview Questions

- **Why are Linux projects important for a DevOps Engineer?**  
  They demonstrate the ability to apply Linux administration, troubleshooting, automation, and system management concepts in practical environments.

- **What should a Linux Administration Toolkit automate?**  
  It can automate common system checks such as system information, storage usage, process monitoring, service health, user information, log analysis, and backups.

- **How can a Bash script be used for system monitoring?**  
  A Bash script can collect information from commands such as `df`, `free`, `ps`, `uptime`, and `systemctl`, then evaluate the results and generate useful alerts or reports.

- **How would you automate backups in Linux?**  
  A script can create timestamped compressed archives using `tar`, store them in a backup directory, verify successful creation, and optionally remove older backups according to a retention policy.

- **How can you monitor disk usage with Bash?**  
  Use `df` to obtain filesystem usage, extract the usage percentage, compare it with a threshold, and generate a warning when the threshold is exceeded.

- **How can you check whether a Linux service is running from a script?**  
  Use:
  ```bash
  systemctl is-active service-name
  ```

- **How can Bash analyze log files?**  
  Commands such as `grep`, `awk`, `sed`, `sort`, `uniq`, and `tail` can be combined to search, count, filter, and summarize log entries.

- **Why should DevOps scripts return meaningful exit codes?**  
  Exit codes allow CI/CD systems, monitoring tools, and other automation to determine whether a command or operation succeeded or failed.

- **How can Linux administration scripts be used in CI/CD?**  
  They can automate tasks such as environment preparation, validation, deployment, health checks, log collection, and cleanup.

- **What skills does the Linux Administration Toolkit demonstrate?**  
  It demonstrates Linux command-line usage, shell scripting, file management, permissions, process management, service management, storage monitoring, logging, and automation.

---

# 📚 Navigation

⬅️ Previous: **[16-Hands-on-Labs.md](16-Hands-on-Labs.md)**

➡️ Next: **[18-Linux-Fundamentals-Checklist.md](18-Linux-Fundamentals-Checklist.md)**

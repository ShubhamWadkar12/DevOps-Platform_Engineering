# 🧪 Linux Hands-on Labs

Hands-on practice is where Linux concepts become practical skills.

These labs combine the topics covered so far:

- Linux Basics
- Linux Architecture
- Linux Distributions
- Boot Process
- Filesystem Hierarchy Standard
- Terminal Navigation
- Essential Linux Commands
- Help Commands
- File Management
- Users and Groups
- Permissions
- Processes and Services
- Storage
- Package Management
- Shell

The goal is to perform common Linux administration tasks from the terminal without depending on a graphical interface.

---

# 🧪 Lab 1 — File Operations

## 🎯 Objective

Practice creating, copying, moving, renaming, searching, and deleting files and directories.

---

## Step 1 — Create Lab Directory

```bash
mkdir -p ~/linux-labs/file-operations
cd ~/linux-labs/file-operations
```

Verify:

```bash
pwd
```

```bash
ls -la
```

---

## Step 2 — Create Directories

Create:

```text
documents/
scripts/
logs/
backup/
```

Command:

```bash
mkdir documents scripts logs backup
```

Verify:

```bash
ls -la
```

---

## Step 3 — Create Files

```bash
touch documents/notes.txt
touch scripts/backup.sh
touch logs/application.log
```

Verify:

```bash
find . -type f
```

---

## Step 4 — Copy a File

Copy the notes file to the backup directory:

```bash
cp documents/notes.txt backup/
```

Verify:

```bash
ls -l backup/
```

---

## Step 5 — Rename a File

```bash
mv backup/notes.txt backup/notes-backup.txt
```

Verify:

```bash
ls -l backup/
```

---

## Step 6 — Create a Symbolic Link

```bash
ln -s "$(pwd)/documents/notes.txt" notes-link.txt
```

Check:

```bash
ls -l
```

---

## Step 7 — Search for Files

Find all text files:

```bash
find . -type f -name "*.txt"
```

Find all log files:

```bash
find . -type f -name "*.log"
```

---

## Step 8 — Check File Information

```bash
file documents/notes.txt
```

```bash
stat documents/notes.txt
```

---

## Step 9 — Create an Archive

```bash
tar -czf file-operations-backup.tar.gz documents scripts logs
```

Verify:

```bash
tar -tf file-operations-backup.tar.gz
```

---

# 🧪 Lab 2 — User Management

## 🎯 Objective

Practice creating users and groups and managing group membership.

---

## Step 1 — Create a Group

```bash
sudo groupadd devops-lab
```

Verify:

```bash
getent group devops-lab
```

---

## Step 2 — Create Users

```bash
sudo useradd -m -s /bin/bash developer1
```

```bash
sudo useradd -m -s /bin/bash developer2
```

Verify:

```bash
id developer1
```

```bash
id developer2
```

---

## Step 3 — Set Passwords

```bash
sudo passwd developer1
```

```bash
sudo passwd developer2
```

Use test passwords only for this lab.

---

## Step 4 — Add Users to Group

```bash
sudo usermod -aG devops-lab developer1
```

```bash
sudo usermod -aG devops-lab developer2
```

Verify:

```bash
groups developer1
```

```bash
groups developer2
```

---

## Step 5 — Inspect User Information

```bash
getent passwd developer1
```

```bash
getent passwd developer2
```

Check IDs:

```bash
id developer1
```

```bash
id developer2
```

---

## Step 6 — Remove a User from the Group

```bash
sudo gpasswd -d developer2 devops-lab
```

Verify:

```bash
groups developer2
```

---

## Step 7 — Clean Up

After completing the lab:

```bash
sudo userdel -r developer1
```

```bash
sudo userdel -r developer2
```

```bash
sudo groupdel devops-lab
```

Verify:

```bash
getent group devops-lab
```

---

# 🧪 Lab 3 — Permission Management

## 🎯 Objective

Practice Linux permissions, ownership, and `chmod`.

---

## Step 1 — Create Lab Directory

```bash
mkdir -p ~/linux-labs/permissions
cd ~/linux-labs/permissions
```

---

## Step 2 — Create Files

```bash
touch application.conf
touch deploy.sh
touch secret.txt
```

Check:

```bash
ls -l
```

---

## Step 3 — Set File Permissions

Configuration file:

```bash
chmod 640 application.conf
```

Deployment script:

```bash
chmod 750 deploy.sh
```

Secret file:

```bash
chmod 600 secret.txt
```

Check:

```bash
ls -l
```

Expected permission concepts:

```text
application.conf → 640
deploy.sh        → 750
secret.txt       → 600
```

---

## Step 4 — Symbolic Permissions

Add execute permission:

```bash
chmod u+x deploy.sh
```

Remove write permission from others:

```bash
chmod o-w application.conf
```

Check:

```bash
ls -l
```

---

## Step 5 — Check Ownership

```bash
ls -l application.conf
```

Detailed information:

```bash
stat application.conf
```

---

## Step 6 — Practice `umask`

Check current umask:

```bash
umask
```

Create a test file:

```bash
touch umask-test.txt
```

Check:

```bash
ls -l umask-test.txt
```

---

# 🧪 Lab 4 — Process Monitoring

## 🎯 Objective

Practice identifying and managing running processes.

---

## Step 1 — View Processes

```bash
ps
```

View all processes:

```bash
ps aux
```

Alternative:

```bash
ps -ef
```

---

## Step 2 — Check PID 1

```bash
ps -p 1 -f
```

Check:

```bash
ps -p 1 -o pid,comm,args
```

---

## Step 3 — Monitor Processes

```bash
top
```

Exit:

```text
q
```

If `htop` is installed:

```bash
htop
```

---

## Step 4 — Start a Background Process

```bash
sleep 600 &
```

Check:

```bash
jobs
```

---

## Step 5 — Find the Process

```bash
pgrep -a sleep
```

---

## Step 6 — Inspect the Process

Replace `<PID>` with the actual PID:

```bash
ps -p <PID> -f
```

Check its state:

```bash
ps -p <PID> -o pid,ppid,stat,cmd
```

---

## Step 7 — Terminate the Process

Send a normal termination request:

```bash
kill <PID>
```

Verify:

```bash
pgrep -a sleep
```

---

# 🧪 Lab 5 — Background Jobs

## 🎯 Objective

Practice foreground and background process management.

---

## Step 1

Start:

```bash
sleep 300
```

Press:

```text
Ctrl + Z
```

---

## Step 2

Check jobs:

```bash
jobs
```

---

## Step 3

Resume in Background

```bash
bg
```

Check:

```bash
jobs
```

---

## Step 4

Bring it Back to Foreground

```bash
fg
```

---

## Step 5

Stop It

Press:

```text
Ctrl + C
```

---

# 🧪 Lab 6 — Service Management

## 🎯 Objective

Practice inspecting and managing Linux services.

---

## Step 1 — Check systemd

```bash
ps -p 1 -f
```

If the system uses systemd, PID 1 should normally be:

```text
systemd
```

---

## Step 2 — List Services

```bash
systemctl list-units --type=service
```

---

## Step 3 — Check SSH Service

Depending on the distribution, the service may be named `ssh` or `sshd`.

Try:

```bash
systemctl status ssh
```

If unavailable:

```bash
systemctl status sshd
```

---

## Step 4 — Check Service State

```bash
systemctl is-active ssh
```

or:

```bash
systemctl is-active sshd
```

---

## Step 5 — View Logs

For SSH:

```bash
journalctl -u ssh
```

or:

```bash
journalctl -u sshd
```

View recent entries:

```bash
journalctl -u ssh -n 50
```

---

## Step 6 — Follow Logs

```bash
journalctl -f
```

Exit with:

```text
Ctrl + C
```

---

# 🧪 Lab 7 — Storage Investigation

## 🎯 Objective

Understand disk devices, filesystems, mount points, disk usage, and inodes.

---

## Step 1 — View Block Devices

```bash
lsblk
```

Detailed filesystem information:

```bash
lsblk -f
```

---

## Step 2 — Check Disk Usage

```bash
df -h
```

---

## Step 3 — Check Inodes

```bash
df -i
```

---

## Step 4 — Check Mount Points

```bash
findmnt
```

---

## Step 5 — Check Filesystem UUIDs

```bash
blkid
```

---

## Step 6 — Inspect `/etc/fstab`

```bash
cat /etc/fstab
```

---

## Step 7 — Check Directory Usage

```bash
du -h --max-depth=1 ~
```

Check logs:

```bash
du -sh /var/log
```

---

# 🧪 Lab 8 — Compression and Archiving

## 🎯 Objective

Practice `tar`, `gzip`, and `zip`.

---

## Step 1 — Create Practice Files

```bash
mkdir -p ~/linux-labs/compression
cd ~/linux-labs/compression
```

Create files:

```bash
touch file1.txt file2.txt file3.txt
```

---

## Step 2 — Create a TAR Archive

```bash
tar -cf files.tar file1.txt file2.txt file3.txt
```

List contents:

```bash
tar -tf files.tar
```

---

## Step 3 — Create a GZIP Compressed Archive

```bash
tar -czf files.tar.gz file1.txt file2.txt file3.txt
```

Check:

```bash
ls -lh
```

List contents:

```bash
tar -tf files.tar.gz
```

---

## Step 4 — Create a ZIP Archive

```bash
zip files.zip file1.txt file2.txt file3.txt
```

List contents:

```bash
unzip -l files.zip
```

---

## Step 5 — Extract Archives

Extract TAR:

```bash
tar -xf files.tar
```

Extract TAR.GZ:

```bash
tar -xzf files.tar.gz
```

Extract ZIP:

```bash
unzip files.zip
```

---

# 🧪 Lab 9 — Package Management

## 🎯 Objective

Practice installing, inspecting, updating, and removing packages.

---

# Ubuntu / Debian

First identify your distribution:

```bash
cat /etc/os-release
```

Update package information:

```bash
sudo apt update
```

Search:

```bash
apt search curl
```

Show package information:

```bash
apt show curl
```

Install:

```bash
sudo apt install curl
```

Check version:

```bash
curl --version
```

Remove:

```bash
sudo apt remove curl
```

Only remove packages you installed for the lab and no longer need.

---

# Fedora / RHEL

If you are using a DNF-based system:

```bash
sudo dnf search curl
```

View information:

```bash
dnf info curl
```

Install:

```bash
sudo dnf install curl
```

Check:

```bash
curl --version
```

Remove:

```bash
sudo dnf remove curl
```

---

# 🧪 Lab 10 — Shell Environment

## 🎯 Objective

Practice environment variables, `PATH`, aliases, and shell configuration.

---

## Step 1 — Check Shell

```bash
echo $SHELL
```

Check the current shell process:

```bash
ps -p $$ -o comm=
```

---

## Step 2 — Check Environment

```bash
printenv
```

---

## Step 3 — Check Important Variables

```bash
echo $HOME
```

```bash
echo $USER
```

```bash
echo $SHELL
```

```bash
echo $PATH
```

---

## Step 4 — Create a Variable

```bash
APP_NAME="DevOps"
```

Print:

```bash
echo $APP_NAME
```

---

## Step 5 — Export a Variable

```bash
export ENVIRONMENT="development"
```

Check:

```bash
echo $ENVIRONMENT
```

---

## Step 6 — Create an Alias

```bash
alias ll='ls -lah'
```

Run:

```bash
ll
```

Remove:

```bash
unalias ll
```

---

# 🧪 Lab 11 — Bash Configuration

## 🎯 Objective

Understand how Bash configuration works.

---

## Step 1

Check:

```bash
ls -la ~
```

Look for:

```text
.bashrc
.profile
```

---

## Step 2

Inspect `.bashrc`:

```bash
cat ~/.bashrc
```

---

## Step 3

Add a Temporary Alias

```bash
alias c='clear'
```

Test:

```bash
c
```

---

## Step 4

Reload Configuration

If you make a change to `.bashrc`:

```bash
source ~/.bashrc
```

---

# 🧪 Lab 12 — Complete Linux Administration Lab

## 🎯 Objective

Combine everything learned so far into one practical workflow.

Imagine you have received a new Linux server for a DevOps project.

Your task is to prepare it for an application deployment.

---

## Step 1 — System Information

Identify:

```bash
hostname
```

```bash
uname -a
```

```bash
cat /etc/os-release
```

```bash
whoami
```

```bash
id
```

---

## Step 2 — Storage

Check:

```bash
lsblk
```

```bash
df -h
```

```bash
df -i
```

---

## Step 3 — Create Application Structure

Create:

```text
/opt/devops-app/
├── app/
├── config/
├── logs/
├── scripts/
└── backup/
```

If you have permission to use `/opt`:

```bash
sudo mkdir -p /opt/devops-app/{app,config,logs,scripts,backup}
```

---

## Step 4 — Create a Service User

Create:

```bash
sudo useradd -r -m -s /usr/sbin/nologin devops-app
```

Check:

```bash
id devops-app
```

> The exact `nologin` path can vary by distribution. Check `/etc/shells` or the filesystem if needed.

---

## Step 5 — Create a Group

```bash
sudo groupadd devops-app
```

If the group already exists, use the existing group rather than recreating it.

---

## Step 6 — Configure Ownership

```bash
sudo chown -R devops-app:devops-app /opt/devops-app
```

Verify:

```bash
ls -la /opt/devops-app
```

---

## Step 7 — Configure Permissions

```bash
sudo chmod -R 750 /opt/devops-app
```

Then verify:

```bash
ls -ld /opt/devops-app
```

---

## Step 8 — Create Application Files

```bash
sudo touch /opt/devops-app/app/application.py
sudo touch /opt/devops-app/config/application.conf
sudo touch /opt/devops-app/logs/application.log
sudo touch /opt/devops-app/scripts/deploy.sh
```

Verify:

```bash
sudo find /opt/devops-app -type f
```

---

## Step 9 — Make Deployment Script Executable

```bash
sudo chmod 750 /opt/devops-app/scripts/deploy.sh
```

Check:

```bash
ls -l /opt/devops-app/scripts/deploy.sh
```

---

## Step 10 — Create Backup

```bash
sudo tar -czf /opt/devops-app/backup/application-backup.tar.gz /opt/devops-app/app /opt/devops-app/config
```

Verify:

```bash
sudo tar -tf /opt/devops-app/backup/application-backup.tar.gz
```

---

## Step 11 — Check Processes

```bash
ps aux
```

Monitor:

```bash
top
```

---

## Step 12 — Check Services

```bash
systemctl list-units --type=service
```

Inspect an appropriate existing service:

```bash
systemctl status <service-name>
```

---

## Step 13 — Check Logs

```bash
journalctl -n 50
```

Follow:

```bash
journalctl -f
```

Exit:

```text
Ctrl + C
```

---

# 🧪 Final Challenge — Linux Server Setup

Complete the following without looking at the previous labs.

## Scenario

You are given a fresh Linux server.

You need to prepare it for a DevOps application.

### Requirements

Create:

```text
/opt/myapp/
├── app/
├── config/
├── logs/
├── scripts/
└── backup/
```

Create a dedicated user:

```text
myapp
```

Create a group:

```text
myapp
```

Configure:

```text
Owner → myapp
Group → myapp
```

Create:

```text
application.py
application.conf
application.log
deploy.sh
```

Set appropriate permissions.

Create a compressed backup.

Check:

```text
Disk usage
Inode usage
File ownership
File permissions
Running processes
Running services
System logs
```

---

# 🎯 Final Verification Checklist

Before completing the Linux Fundamentals section, verify that you can perform these tasks without searching for commands.

## Linux Basics

- [ ] Explain what Linux is
- [ ] Explain Linux architecture
- [ ] Identify your Linux distribution
- [ ] Explain the Linux boot process
- [ ] Explain the FHS

## Navigation

- [ ] Use `pwd`
- [ ] Use `ls`
- [ ] Use `cd`
- [ ] Navigate using absolute paths
- [ ] Navigate using relative paths

## Commands

- [ ] Use `man`
- [ ] Use `help`
- [ ] Use `--help`
- [ ] Use `which` / `command -v`
- [ ] Use `history`

## File Management

- [ ] Create files
- [ ] Create directories
- [ ] Copy files
- [ ] Move files
- [ ] Rename files
- [ ] Delete files
- [ ] Create symbolic links
- [ ] Find files
- [ ] Search file contents

## Users and Groups

- [ ] Create users
- [ ] Create groups
- [ ] Add users to groups
- [ ] Remove users from groups
- [ ] Check UID/GID
- [ ] Understand `/etc/passwd`
- [ ] Understand `/etc/shadow`
- [ ] Understand `/etc/group`

## Permissions

- [ ] Understand `rwx`
- [ ] Understand owner/group/others
- [ ] Use `chmod`
- [ ] Use `chown`
- [ ] Use `chgrp`
- [ ] Understand numeric permissions
- [ ] Understand `umask`
- [ ] Understand SUID
- [ ] Understand SGID
- [ ] Understand sticky bit

## Processes

- [ ] Use `ps`
- [ ] Use `top`
- [ ] Use `htop`
- [ ] Find processes
- [ ] Understand PID
- [ ] Understand PPID
- [ ] Use `kill`
- [ ] Understand process states
- [ ] Manage background jobs

## Services

- [ ] Understand systemd
- [ ] Use `systemctl`
- [ ] Start a service
- [ ] Stop a service
- [ ] Restart a service
- [ ] Enable a service
- [ ] Check service status
- [ ] Use `journalctl`

## Storage

- [ ] Use `lsblk`
- [ ] Understand partitions
- [ ] Understand filesystems
- [ ] Understand mounting
- [ ] Use `df`
- [ ] Use `du`
- [ ] Check inode usage
- [ ] Understand `/etc/fstab`

## Compression

- [ ] Use `tar`
- [ ] Use `gzip`
- [ ] Use `zip`
- [ ] Extract archives
- [ ] Create compressed backups

## Package Management

- [ ] Identify package manager
- [ ] Search packages
- [ ] Install packages
- [ ] Update packages
- [ ] Remove packages
- [ ] Understand dependencies
- [ ] Understand repositories

## Shell

- [ ] Understand Bash
- [ ] Use environment variables
- [ ] Understand `PATH`
- [ ] Create aliases
- [ ] Understand `.bashrc`
- [ ] Use pipes
- [ ] Use redirection
- [ ] Understand exit codes
- [ ] Run background commands

---

# 💼 Interview Questions

- **Why are hands-on Linux labs important for a DevOps Engineer?**  
  They turn theoretical Linux knowledge into practical skills required for server administration, troubleshooting, automation, deployments, and infrastructure management.

- **How would you prepare a new Linux server for an application?**  
  Identify the OS and hardware, update packages, configure users and groups, create application directories, configure permissions, install required software, configure services, verify storage, and establish monitoring and logging.

- **How would you troubleshoot a server running out of disk space?**  
  Start with `df -h`, check inode usage with `df -i`, identify large directories with `du`, locate large files, and investigate logs, caches, and application data before deciding what can safely be removed.

- **How would you troubleshoot an application that is not running?**  
  Check the service with `systemctl status`, inspect logs with `journalctl`, inspect processes with `ps` or `pgrep`, check ports with `ss`, verify configuration and permissions, and test the application.

- **How would you securely give an application access to its files?**  
  Create a dedicated service account, assign appropriate ownership and group membership, and grant only the permissions required by the application.

- **Why should applications avoid running as root?**  
  Running applications as root gives them excessive privileges. A dedicated non-root service account limits the potential impact of application vulnerabilities or mistakes.

- **How would you automate Linux server setup?**  
  Server setup can be automated using Bash scripts, cloud-init, Ansible, Terraform provisioning, and CI/CD pipelines.

- **What Linux skills are most important for DevOps?**  
  Command-line navigation, file management, permissions, users and groups, processes, services, storage, networking, package management, shell scripting, troubleshooting, and automation.

---

# 📚 Navigation

⬅️ Previous: **[15-Shell.md](15-Shell.md)**

➡️ Next: **[17-Mini-Projects.md](17-Mini-Projects.md)**

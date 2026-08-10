# ⌨️ Essential Linux Commands


Linux is primarily managed through the command line. As a DevOps Engineer, you will regularly use commands to inspect the system, manage files, monitor resources, work with processes, and troubleshoot servers.

This chapter covers the essential commands you should be comfortable using before moving into advanced Linux administration.

---

# 📌 Command Categories

The essential commands in this section are grouped into:

- System Information
- File and Directory Operations
- Text and Output
- Searching
- Disk and Storage
- Processes
- Networking
- Users
- Archives and Compression
- System and Services

---

# 🖥️ System Information

## `uname`

Displays system information.

```bash
uname
```

Display the Kernel version:

```bash
uname -r
```

Display detailed system information:

```bash
uname -a
```

---

## `hostname`

Displays the system hostname.

```bash
hostname
```

Set or change the hostname using the appropriate system configuration tools rather than relying on a temporary shell-only change.

---

## `whoami`

Displays the currently logged-in username.

```bash
whoami
```

Example:

```text
shubham
```

---

## `id`

Displays user and group information.

```bash
id
```

Example:

```text
uid=1000(shubham) gid=1000(shubham) groups=1000(shubham),27(sudo)
```

---

## `date`

Displays the current date and time.

```bash
date
```

---

## `uptime`

Shows how long the system has been running and provides basic load information.

```bash
uptime
```

---

# 📂 File and Directory Commands

## `pwd`

Displays the current working directory.

```bash
pwd
```

---

## `ls`

Lists files and directories.

```bash
ls
```

Useful options:

```bash
ls -l
ls -a
ls -h
ls -lah
```

---

## `cd`

Changes the current directory.

```bash
cd /var/log
```

Go to the home directory:

```bash
cd ~
```

Go to the previous directory:

```bash
cd -
```

Go to the parent directory:

```bash
cd ..
```

---

## `mkdir`

Creates a directory.

```bash
mkdir DevOps
```

Create nested directories:

```bash
mkdir -p DevOps/Linux/Practice
```

---

## `touch`

Creates an empty file or updates a file's timestamps.

```bash
touch notes.txt
```

---

## `cp`

Copies files or directories.

Copy a file:

```bash
cp file.txt backup.txt
```

Copy a directory:

```bash
cp -r project project-backup
```

---

## `mv`

Moves or renames files and directories.

Rename a file:

```bash
mv old.txt new.txt
```

Move a file:

```bash
mv notes.txt /tmp/
```

---

## `rm`

Removes files or directories.

Remove a file:

```bash
rm notes.txt
```

Remove an empty directory:

```bash
rmdir directory
```

Remove a directory and its contents:

```bash
rm -r directory
```

Use recursive deletion carefully, especially with elevated privileges.

---

# 📖 Reading Files

## `cat`

Displays file contents.

```bash
cat notes.txt
```

Combine multiple files:

```bash
cat file1.txt file2.txt
```

---

## `less`

Views large files page by page.

```bash
less application.log
```

Useful keys:

```text
Space  → Next page
b      → Previous page
/word  → Search
q      → Quit
```

`less` is particularly useful for large log files.

---

## `head`

Displays the beginning of a file.

```bash
head file.txt
```

Show the first 5 lines:

```bash
head -n 5 file.txt
```

---

## `tail`

Displays the end of a file.

```bash
tail file.txt
```

Show the last 20 lines:

```bash
tail -n 20 application.log
```

Follow a log file in real time:

```bash
tail -f application.log
```

This is extremely useful when troubleshooting applications.

---

# 🔎 Searching

## `grep`

Searches text for a pattern.

```bash
grep "error" application.log
```

Case-insensitive search:

```bash
grep -i "error" application.log
```

Search recursively:

```bash
grep -r "error" /var/log
```

Show line numbers:

```bash
grep -n "error" application.log
```

---

## `find`

Searches for files and directories.

Find a file by name:

```bash
find /home -name "notes.txt"
```

Find `.log` files:

```bash
find /var/log -name "*.log"
```

Find directories:

```bash
find . -type d
```

Find files:

```bash
find . -type f
```

---

## `which`

Shows the location of a command.

```bash
which bash
```

Example:

```text
/usr/bin/bash
```

For shell command lookup, `command -v` is also useful:

```bash
command -v python3
```

---

# 📊 Disk and Storage

## `df`

Displays filesystem disk usage.

```bash
df -h
```

`-h` displays sizes in a human-readable format.

---

## `du`

Shows disk usage of files and directories.

```bash
du -sh directory
```

Example:

```bash
du -sh /var/log
```

Find the size of directories:

```bash
du -h --max-depth=1
```

---

## `lsblk`

Displays block devices and storage information.

```bash
lsblk
```

Useful when working with:

- Disks
- Partitions
- Volumes
- Cloud storage

---

# ⚙️ Process Management

## `ps`

Displays running processes.

```bash
ps
```

Show processes for all users:

```bash
ps aux
```

---

## `top`

Provides a real-time view of processes and system resource usage.

```bash
top
```

It can help you identify:

- CPU usage
- Memory usage
- Running processes
- Process IDs

---

## `htop`

An interactive alternative to `top`.

```bash
htop
```

It may need to be installed separately depending on the distribution.

---

## `kill`

Sends a signal to a process.

```bash
kill PID
```

Example:

```bash
kill 1234
```

A common termination signal is:

```bash
kill -15 1234
```

Forceful termination:

```bash
kill -9 1234
```

Use `SIGKILL` (`-9`) only when necessary because it does not allow the process to clean up normally.

---

## `jobs`

Displays jobs started by the current shell.

```bash
jobs
```

---

## `bg`

Continues a stopped job in the background.

```bash
bg
```

---

## `fg`

Brings a background job to the foreground.

```bash
fg
```

---

# 🧠 Memory and System Resources

## `free`

Displays memory usage.

```bash
free -h
```

Shows:

- Total memory
- Used memory
- Available memory
- Swap

---

## `vmstat`

Displays information about processes, memory, paging, and CPU activity.

```bash
vmstat
```

Example:

```bash
vmstat 2
```

This updates the output every 2 seconds.

---

# 🌐 Networking Commands

## `ip`

Modern command for inspecting and managing network interfaces, addresses, routes, and more.

Show network interfaces:

```bash
ip addr
```

Show routes:

```bash
ip route
```

---

## `ping`

Tests network connectivity using ICMP.

```bash
ping google.com
```

---

## `curl`

Transfers data using URLs and is widely used for testing HTTP APIs and services.

Example:

```bash
curl https://example.com
```

Check HTTP headers:

```bash
curl -I https://example.com
```

---

## `ss`

Displays network sockets.

```bash
ss
```

Show listening TCP/UDP sockets:

```bash
ss -tuln
```

This is useful for checking which ports are listening.

---

## `dig`

Performs DNS queries.

```bash
dig example.com
```

---

## `nslookup`

Performs DNS lookups.

```bash
nslookup example.com
```

`dig` is generally preferred for detailed DNS troubleshooting, but `nslookup` is still useful and widely encountered.

---

# 👤 User Commands

## `who`

Shows users currently logged in.

```bash
who
```

---

## `w`

Shows logged-in users and what they are doing.

```bash
w
```

---

## `last`

Shows login history.

```bash
last
```

---

## `sudo`

Runs a command with elevated privileges according to the system's sudo policy.

Example:

```bash
sudo apt update
```

Use `sudo` carefully, especially when executing commands that modify or delete system files.

---

# 📦 Archives and Compression

## `tar`

Creates and extracts archive files.

Create an archive:

```bash
tar -cf backup.tar project/
```

Create a gzip-compressed archive:

```bash
tar -czf backup.tar.gz project/
```

Extract an archive:

```bash
tar -xf backup.tar
```

Extract a `.tar.gz` archive:

```bash
tar -xzf backup.tar.gz
```

List archive contents:

```bash
tar -tf backup.tar
```

---

## `gzip`

Compresses files.

```bash
gzip file.txt
```

Decompress:

```bash
gunzip file.txt.gz
```

---

## `zip`

Creates ZIP archives.

```bash
zip backup.zip file.txt
```

Create a ZIP archive from a directory:

```bash
zip -r backup.zip project/
```

Extract:

```bash
unzip backup.zip
```

---

# 🔗 Symbolic Links

## `ln`

Creates links.

Create a symbolic link:

```bash
ln -s /path/to/original link-name
```

Example:

```bash
ln -s /var/log/application.log app.log
```

Symbolic links are commonly used for configuration, application deployments, and filesystem organization.

---

# 🧰 System and Service Commands

## `systemctl`

Manages systemd services.

Check service status:

```bash
systemctl status nginx
```

Start a service:

```bash
sudo systemctl start nginx
```

Stop a service:

```bash
sudo systemctl stop nginx
```

Restart a service:

```bash
sudo systemctl restart nginx
```

Enable a service at boot:

```bash
sudo systemctl enable nginx
```

---

## `journalctl`

Views logs collected by the systemd journal.

View current logs:

```bash
journalctl
```

View logs for the current boot:

```bash
journalctl -b
```

Follow logs:

```bash
journalctl -f
```

View logs for a specific service:

```bash
journalctl -u nginx
```

---

# 🔄 Common DevOps Troubleshooting Flow

When a Linux application is not responding, you can combine several commands:

```bash
ps aux
```

Check processes.

```bash
top
```

Check CPU and memory.

```bash
df -h
```

Check disk space.

```bash
ss -tuln
```

Check listening ports.

```bash
systemctl status nginx
```

Check service status.

```bash
journalctl -u nginx
```

Check service logs.

```bash
curl http://localhost
```

Test the application.

This is the beginning of real Linux troubleshooting.

---

# 🛠️ Hands-on Practice

Practice these commands in your Linux environment:

```bash
pwd
ls -lah
whoami
id
uname -r
hostname
uptime
date
```

Create and manage files:

```bash
mkdir linux-practice
cd linux-practice
touch notes.txt
cp notes.txt backup.txt
mv backup.txt backup-notes.txt
ls -lah
```

Read files:

```bash
cat notes.txt
head notes.txt
tail notes.txt
```

Search:

```bash
grep "Linux" notes.txt
find . -type f
```

Check system resources:

```bash
free -h
df -h
ps
```

Check networking:

```bash
ip addr
ip route
ss -tuln
```

---

# 🧪 Practice Challenge

Create this structure:

```text
linux-practice/
├── notes/
│   ├── linux.txt
│   └── commands.txt
├── logs/
└── backup/
```

Then:

1. Create the directories.
2. Create both files.
3. Add some text to `linux.txt`.
4. Copy `linux.txt` into `backup/`.
5. Rename the copied file.
6. Search for a word using `grep`.
7. Find all files using `find`.
8. Check disk usage using `du`.
9. Create a compressed archive using `tar`.
10. Verify the archive contents.

---

# 💼 Interview Questions

- **What is the difference between `df` and `du`?**  
  `df` shows filesystem-level disk usage, while `du` shows the disk space used by files and directories.

- **What is the difference between `cp` and `mv`?**  
  `cp` copies files or directories, while `mv` moves or renames them.

- **What is the difference between `rm` and `rmdir`?**  
  `rm` removes files and can recursively remove directories with the appropriate option. `rmdir` removes empty directories.

- **What is the difference between `grep` and `find`?**  
  `grep` searches for text patterns inside files, while `find` searches for files and directories based on properties such as name, type, or location.

- **What is the difference between `ps` and `top`?**  
  `ps` provides a snapshot of processes, while `top` provides an interactive, continuously updating view.

- **What is the purpose of `kill`?**  
  `kill` sends a signal to a process, allowing you to request termination or perform other signal-based actions.

- **What is the purpose of `curl` in DevOps?**  
  `curl` is commonly used to test HTTP endpoints, APIs, downloads, and connectivity.

- **What is the purpose of `ss`?**  
  `ss` displays socket and network connection information and is commonly used to inspect listening ports and active connections.

- **What is the purpose of `tar`?**  
  `tar` creates and extracts archive files and is commonly used for backups and packaging files.

- **What is the difference between `systemctl` and `journalctl`?**  
  `systemctl` manages and inspects systemd units and services, while `journalctl` is used to query logs stored in the systemd journal.

- **How would you check whether a service is running?**  
  Use `systemctl status service-name`.

- **How would you check which ports are listening on a Linux server?**  
  Use `ss -tuln`.

- **How would you check available disk space?**  
  Use `df -h`.

- **How would you check memory usage?**  
  Use `free -h`.

- **How would you monitor running processes?**  
  Use `top`, `htop`, or commands such as `ps`.

- **How would you troubleshoot a web server that is not responding?**  
  Check the service with `systemctl`, inspect logs with `journalctl`, check listening ports with `ss`, verify resources with `top`/`free`/`df`, and test the service using `curl`.

---

# 📚 Navigation

⬅️ Previous: **[06-Terminal-Navigation.md](06-Terminal-Navigation.md)**

➡️ Next: **[08-Help-Commands.md](08-Help-Commands.md)**

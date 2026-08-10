# 📁 File Management

File management is one of the most important Linux fundamentals.

As a DevOps Engineer, you will constantly create, copy, move, rename, delete, inspect, search, archive, and organize files and directories.

You'll use these skills while working with:

- Application files
- Configuration files
- Logs
- Scripts
- Backups
- Deployment artifacts
- Docker files
- CI/CD pipelines
- Infrastructure code

---

# 📌 Linux Files

In Linux, almost everything is represented through the filesystem.

Examples include:

- Regular files
- Directories
- Symbolic links
- Device files
- Sockets
- Named pipes

You can inspect a file using:

```bash
file filename
```

Example:

```bash
file script.sh
```

---

# 📂 Creating Directories

## `mkdir`

Creates a directory.

```bash
mkdir project
```

Create multiple directories:

```bash
mkdir logs backups scripts
```

Create nested directories:

```bash
mkdir -p project/src/config
```

The `-p` option creates parent directories when they don't already exist.

---

# 📄 Creating Files

## `touch`

Creates an empty file if it doesn't exist.

```bash
touch notes.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

`touch` can also update the timestamps of an existing file.

---

# 👀 Viewing Files

## `cat`

Displays the contents of a file.

```bash
cat notes.txt
```

For multiple files:

```bash
cat file1.txt file2.txt
```

---

## `less`

Used to read large files interactively.

```bash
less application.log
```

Useful keys:

```text
Space → Next page
b     → Previous page
/word → Search
n     → Next match
N     → Previous match
q     → Quit
```

For large logs, `less` is generally more practical than `cat`.

---

## `head`

Displays the beginning of a file.

```bash
head notes.txt
```

Show the first 5 lines:

```bash
head -n 5 notes.txt
```

---

## `tail`

Displays the end of a file.

```bash
tail notes.txt
```

Show the last 20 lines:

```bash
tail -n 20 application.log
```

Follow a log continuously:

```bash
tail -f application.log
```

This is commonly used for real-time troubleshooting.

---

# 📋 Copying Files and Directories

## `cp`

Copies files and directories.

Copy a file:

```bash
cp notes.txt backup.txt
```

Copy a file into another directory:

```bash
cp notes.txt backups/
```

Copy multiple files:

```bash
cp file1.txt file2.txt backups/
```

Copy a directory recursively:

```bash
cp -r project project-backup
```

---

# 🚚 Moving and Renaming

## `mv`

`mv` is used to:

- Move files
- Move directories
- Rename files
- Rename directories

Rename a file:

```bash
mv old.txt new.txt
```

Move a file:

```bash
mv notes.txt /tmp/
```

Move and rename:

```bash
mv notes.txt /backup/notes-old.txt
```

Rename a directory:

```bash
mv project old-project
```

---

# 🗑️ Removing Files

## `rm`

Removes files.

```bash
rm notes.txt
```

Remove multiple files:

```bash
rm file1.txt file2.txt
```

Remove a directory and its contents:

```bash
rm -r project
```

Force removal:

```bash
rm -f file.txt
```

Recursive and force removal:

```bash
rm -rf project
```

⚠️ **Be extremely careful with `rm -rf`.**

A mistaken command can permanently delete large amounts of data.

Never blindly run:

```bash
rm -rf /
```

or commands containing variables or wildcards unless you fully understand what they will affect.

---

# 📁 Removing Empty Directories

## `rmdir`

Removes empty directories.

```bash
rmdir old-directory
```

If the directory contains files, `rmdir` will not remove it.

---

# 🔗 Symbolic Links

## `ln`

Linux supports links between files.

Create a symbolic link:

```bash
ln -s /path/to/original link-name
```

Example:

```bash
ln -s /var/log/application.log app.log
```

Check the link:

```bash
ls -l app.log
```

You may see:

```text
app.log -> /var/log/application.log
```

Symbolic links are commonly used for:

- Configuration
- Application versions
- Deployment directories
- Shared resources

---

# 🔍 Finding Files

## `find`

Searches for files and directories.

Find a file by name:

```bash
find /home -name "notes.txt"
```

Find all `.log` files:

```bash
find /var/log -name "*.log"
```

Find files:

```bash
find . -type f
```

Find directories:

```bash
find . -type d
```

Find files modified recently:

```bash
find . -type f -mtime -1
```

Find files larger than 100 MB:

```bash
find . -type f -size +100M
```

---

# 🔎 Searching Inside Files

## `grep`

`grep` searches for text patterns inside files.

Example:

```bash
grep "error" application.log
```

Case-insensitive search:

```bash
grep -i "error" application.log
```

Show line numbers:

```bash
grep -n "error" application.log
```

Search recursively:

```bash
grep -r "error" /var/log
```

Combine `find` and `grep`:

```bash
find . -type f -name "*.log" -exec grep -H "error" {} \;
```

---

# 📝 Editing Files

Linux provides many text editors.

Common editors include:

- `vim`
- `nano`
- `emacs`

For example:

```bash
nano notes.txt
```

or:

```bash
vim notes.txt
```

As a DevOps Engineer, you should become comfortable with at least one terminal-based editor.

`vim` is especially common on Linux servers.

---

# 📊 File Information

## `file`

Determines the type of a file.

```bash
file script.sh
```

Example:

```text
script.sh: Bourne-Again shell script
```

---

## `stat`

Displays detailed file metadata.

```bash
stat notes.txt
```

It can show:

- File size
- Permissions
- Owner
- Group
- Access time
- Modification time
- Change time
- Inode information

---

# 🕒 File Timestamps

Linux tracks several important timestamps.

### Access Time

When the file was last accessed.

### Modification Time

When the contents were last modified.

### Change Time

When the file's metadata changed.

You can view these using:

```bash
stat file.txt
```

---

# 🔐 File Permissions

File permissions determine who can:

- Read
- Write
- Execute

Example:

```bash
ls -l script.sh
```

Output:

```text
-rwxr-xr-- 1 user user 1200 Aug 10 script.sh
```

The detailed permission model will be covered separately in the Linux Users and Permissions section.

---

# 👤 File Ownership

Every file normally has:

- An owner
- A group

Check ownership:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 shubham devops 1200 Aug 10 notes.txt
```

Here:

```text
shubham → Owner
devops  → Group
```

Ownership management will be covered in detail in the permissions section.

---

# 📦 Archives

## `tar`

`tar` is commonly used to create and extract archives.

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

Extract a gzip-compressed archive:

```bash
tar -xzf backup.tar.gz
```

List archive contents:

```bash
tar -tf backup.tar
```

---

# 🗜️ Compression

## `gzip`

Compress a file:

```bash
gzip file.txt
```

This creates:

```text
file.txt.gz
```

Decompress:

```bash
gunzip file.txt.gz
```

---

## `zip`

Create a ZIP archive:

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

# 📏 Disk Usage

## `du`

Displays disk usage of files and directories.

Check the size of a directory:

```bash
du -sh project/
```

Check sizes of directories in the current location:

```bash
du -h --max-depth=1
```

---

## `df`

Displays filesystem-level disk usage.

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use%
/dev/sda1       100G   45G   55G  45%
```

Remember:

```text
df → Filesystem disk usage
du → File/directory disk usage
```

---

# 🔄 File Management Workflow

A common workflow might look like:

```text
Create
  ↓
Inspect
  ↓
Edit
  ↓
Copy / Move
  ↓
Archive
  ↓
Backup
  ↓
Deploy
  ↓
Monitor
  ↓
Clean Up
```

These operations appear constantly in DevOps workflows.

---

# 🌍 Real-World DevOps Example

Imagine you're deploying a new version of an application.

You might have:

```text
/opt/myapp/
├── current/
├── releases/
│   ├── v1/
│   ├── v2/
│   └── v3/
├── logs/
└── config/
```

A deployment could involve:

1. Copying the new release.
2. Extracting an application archive.
3. Updating configuration files.
4. Creating or updating a symbolic link.
5. Restarting the service.
6. Checking logs.

For example:

```bash
tar -xzf application-v2.tar.gz
```

Then:

```bash
ln -sfn /opt/myapp/releases/v2 /opt/myapp/current
```

Then:

```bash
systemctl restart myapp
```

Finally:

```bash
journalctl -u myapp
```

This demonstrates how basic Linux file management becomes part of a real deployment workflow.

---

# 🛠️ Hands-on Practice

Create a practice environment:

```bash
mkdir -p ~/linux-file-management/{documents,logs,backup,scripts}
```

Move into it:

```bash
cd ~/linux-file-management
```

Create files:

```bash
touch documents/notes.txt
touch logs/application.log
touch scripts/backup.sh
```

Verify:

```bash
find . -type f
```

Copy a file:

```bash
cp documents/notes.txt backup/
```

Rename it:

```bash
mv backup/notes.txt backup/notes-backup.txt
```

Create a symbolic link:

```bash
ln -s "$(pwd)/documents/notes.txt" notes-link.txt
```

Check it:

```bash
ls -l
```

Create an archive:

```bash
tar -czf linux-file-management.tar.gz documents logs scripts
```

Check the archive:

```bash
tar -tf linux-file-management.tar.gz
```

Check directory size:

```bash
du -sh .
```

---

# 🧪 Practice Challenge

Without copying the exact commands from above:

1. Create a directory named `devops-lab`.
2. Inside it create:
   - `scripts`
   - `logs`
   - `backup`
   - `config`
3. Create three files inside different directories.
4. Copy one file into `backup`.
5. Rename the copied file.
6. Create a symbolic link to one of the files.
7. Find all `.log` files using `find`.
8. Search for the word `error` using `grep`.
9. Create a compressed `.tar.gz` archive.
10. Verify the archive contents.
11. Check the size using `du`.
12. Inspect a file's metadata using `stat`.

---

# ⚠️ File Management Safety

Be careful when modifying production systems.

Before destructive commands:

```bash
rm
rm -r
rm -rf
mv
```

verify:

```bash
pwd
ls
```

For potentially dangerous wildcards, inspect what will match before deleting or modifying files.

Avoid running commands with `sudo` unless elevated privileges are actually required.

A good DevOps habit is:

> **Inspect first, modify second.**

---

# 💼 Interview Questions

- **What is the difference between `cp` and `mv`?**  
  `cp` copies files or directories, while `mv` moves or renames them.

- **How do you create a directory in Linux?**  
  Use `mkdir`. For nested directories, use `mkdir -p`.

- **How do you create an empty file?**  
  Use `touch filename`.

- **How do you remove a file?**  
  Use `rm filename`.

- **How do you remove an empty directory?**  
  Use `rmdir directory`.

- **What is the difference between `rm -r` and `rm -rf`?**  
  `rm -r` recursively removes directories and their contents. `-f` forces removal without interactive prompts for many cases. `rm -rf` should be used with extreme caution.

- **What is a symbolic link?**  
  A symbolic link is a special filesystem object that points to another file or directory.

- **How do you create a symbolic link?**  
  Use:
  ```bash
  ln -s target link-name
  ```

- **What is the purpose of `find`?**  
  `find` searches for files and directories based on conditions such as name, type, size, and modification time.

- **What is the purpose of `grep`?**  
  `grep` searches text for patterns inside files or command output.

- **What is the difference between `df` and `du`?**  
  `df` shows filesystem-level disk usage, while `du` shows the space consumed by files and directories.

- **What is the purpose of `stat`?**  
  `stat` displays detailed metadata about a file or filesystem object.

- **What is the difference between `cat`, `less`, `head`, and `tail`?**  
  `cat` displays file contents, `less` provides interactive viewing, `head` shows the beginning, and `tail` shows the end of a file.

- **How do you monitor a log file in real time?**  
  A common approach is:
  ```bash
  tail -f application.log
  ```
  For systemd-managed services, `journalctl -f` can also be used.

- **How would file management be used in DevOps?**  
  DevOps engineers manage application files, configuration, logs, scripts, backups, deployment artifacts, and infrastructure files regularly.

---

# 📚 Navigation

⬅️ Previous: **[08-Help-Commands.md](08-Help-Commands.md)**

➡️ Next: **[10-Users-and-Groups.md](10-Users-and-Groups.md)**

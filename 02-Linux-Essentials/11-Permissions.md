# 🔐 Linux Permissions


Linux permissions control who can access files and directories and what actions they are allowed to perform.

The three basic permissions are:

- **Read (`r`)**
- **Write (`w`)**
- **Execute (`x`)**

Permissions are fundamental to Linux security and are heavily used in DevOps environments for:

- Application files
- Configuration files
- SSH keys
- Deployment scripts
- CI/CD runners
- Service accounts
- Shared directories
- Production servers

---

# 📌 Why Linux Permissions Matter

Linux is a multi-user operating system.

Different users may need different levels of access to the same files.

For example:

```text
Developer
   ↓
Read application source

DevOps Engineer
   ↓
Read + Modify deployment files

Application Service
   ↓
Read configuration

Unauthorized User
   ↓
No access
```

Permissions help enforce these access boundaries.

---

# 📁 Checking Permissions

Use:

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 shubham devops 1200 Aug 10 deploy.sh
```

The first section:

```text
-rwxr-xr--
```

represents the file type and permissions.

---

# 🧩 Understanding Permission Structure

Consider:

```text
-rwxr-xr--
```

Break it down:

```text
- rwx r-x r--
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File type
```

So:

```text
Owner  → rwx
Group  → r-x
Others → r--
```

---

# 📄 File Type

The first character represents the file type.

Common values include:

| Symbol | Meaning |
|---|---|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `s` | Socket |
| `p` | Named pipe |

Example:

```text
-rw-r--r--
```

The first character `-` means it is a regular file.

Example:

```text
drwxr-xr-x
```

The first character `d` means it is a directory.

---

# 🔤 Basic Permissions

## Read — `r`

Allows reading the contents of a file.

For a file:

```text
r → Read contents
```

For a directory:

```text
r → List directory entries
```

---

## Write — `w`

Allows modifying a file.

For a file:

```text
w → Modify contents
```

For a directory:

```text
w → Create, delete, or rename directory entries
```

Directory write permission is especially important because deleting a file is controlled primarily by permissions on the parent directory.

---

## Execute — `x`

For a file:

```text
x → Execute the file as a program
```

For a directory:

```text
x → Traverse/access entries within the directory
```

For directories, `x` is different from "running" the directory.

---

# 👤 Owner, Group, and Others

Linux permissions are traditionally divided into three access classes:

```text
Owner
Group
Others
```

Example:

```text
-rwxr-x---
```

Means:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

---

# 🔢 Numeric Permissions

Linux permissions can also be represented using numbers.

```text
Read    = 4
Write   = 2
Execute = 1
```

Add them together.

### Read only

```text
4
```

### Read + Write

```text
4 + 2 = 6
```

### Read + Execute

```text
4 + 1 = 5
```

### Read + Write + Execute

```text
4 + 2 + 1 = 7
```

---

# 📊 Permission Number Table

| Permission | Value |
|---|---:|
| `---` | 0 |
| `--x` | 1 |
| `-w-` | 2 |
| `-wx` | 3 |
| `r--` | 4 |
| `r-x` | 5 |
| `rw-` | 6 |
| `rwx` | 7 |

---

# 🔢 Example: `755`

Consider:

```text
755
```

Break it down:

```text
7 → Owner
5 → Group
5 → Others
```

Therefore:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

Equivalent symbolic permission:

```text
rwxr-xr-x
```

---

# 🔢 Example: `644`

```text
644
```

Means:

```text
Owner  → rw-
Group  → r--
Others → r--
```

Equivalent:

```text
rw-r--r--
```

This is a common permission setting for ordinary text or configuration files where the owner can modify the file and others can only read it.

---

# 🔐 Changing Permissions with `chmod`

`chmod` means:

**Change Mode**

It changes file and directory permissions.

---

# 🔢 Numeric `chmod`

Example:

```bash
chmod 755 script.sh
```

This gives:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

Another example:

```bash
chmod 644 config.txt
```

Gives:

```text
Owner  → rw-
Group  → r--
Others → r--
```

---

# 🔤 Symbolic `chmod`

Permissions can also be changed using symbolic notation.

Add execute permission for the owner:

```bash
chmod u+x script.sh
```

Where:

```text
u → User/Owner
g → Group
o → Others
a → All
```

Add read permission for the group:

```bash
chmod g+r file.txt
```

Remove write permission from others:

```bash
chmod o-w file.txt
```

Add execute permission for everyone:

```bash
chmod a+x script.sh
```

---

# 🧩 Symbolic Permission Operators

| Operator | Meaning |
|---|---|
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set exact permission |

Examples:

```bash
chmod u+x script.sh
```

```bash
chmod g-w file.txt
```

```bash
chmod o=r file.txt
```

---

# 📂 Directory Permissions

Directory permissions behave differently from file permissions.

For a directory:

```text
r → List contents
w → Create/delete/rename entries
x → Traverse/access entries
```

For example:

```bash
chmod 750 project/
```

Means:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

---

# ⚠️ Why Directory `x` Matters

Suppose a directory has:

```text
r--
```

A user may be able to see directory entries in some situations but cannot properly traverse into the directory without execute permission.

This is why directory permissions should always be understood as:

```text
r → Can list
w → Can modify directory entries
x → Can traverse
```

---

# 👥 Changing Ownership

Permissions and ownership work together.

Use:

```bash
chown
```

to change file ownership.

Example:

```bash
sudo chown shubham file.txt
```

Change owner and group:

```bash
sudo chown shubham:devops file.txt
```

Change ownership recursively:

```bash
sudo chown -R shubham:devops project/
```

Be extremely careful with recursive ownership changes on system directories.

---

# 👥 Changing Group Ownership

Use:

```bash
chgrp
```

Example:

```bash
sudo chgrp devops file.txt
```

Check the result:

```bash
ls -l file.txt
```

---

# 📌 `chmod` vs `chown` vs `chgrp`

| Command | Purpose |
|---|---|
| `chmod` | Change permissions |
| `chown` | Change owner and/or group |
| `chgrp` | Change group ownership |

Example:

```bash
chmod 640 config.yml
```

Changes permissions.

```bash
chown shubham:devops config.yml
```

Changes ownership.

```bash
chgrp devops config.yml
```

Changes the group.

---

# 🛡️ Special Permissions

Linux also supports special permission bits:

- SUID
- SGID
- Sticky Bit

These are important for understanding Linux security and shared environments.

---

# 🔑 SUID

**SUID (Set User ID)** allows an executable file to run with the privileges of the file owner.

A common example is:

```bash
ls -l /usr/bin/passwd
```

You may see an `s` in the owner's execute position.

SUID should be treated carefully because incorrectly configured SUID executables can create security risks.

---

# 👥 SGID

**SGID (Set Group ID)** has different behavior depending on whether it is applied to a file or directory.

For an executable file, it can cause the program to run with the file's group privileges.

For a directory, newly created files can inherit the directory's group ownership.

This is useful for shared project directories.

Example:

```bash
chmod g+s shared/
```

---

# 📌 Sticky Bit

The sticky bit is commonly used on shared directories.

A classic example is:

```text
/tmp
```

The sticky bit allows users to create files in a shared directory while preventing them from deleting or renaming files owned by other users, subject to the system's permission rules.

You may see:

```text
drwxrwxrwt
```

The final `t` represents the sticky bit.

---

# 🔢 Special Permission Numbers

Special permission bits can be represented numerically.

```text
SUID       = 4
SGID       = 2
Sticky Bit = 1
```

Example:

```bash
chmod 4755 program
```

The leading `4` sets SUID.

Example:

```bash
chmod 2775 shared/
```

The leading `2` sets SGID.

Example:

```bash
chmod 1777 shared/
```

The leading `1` sets the sticky bit.

---

# 📌 `umask`

`umask` controls the default permission bits that are removed when new files and directories are created.

Check the current value:

```bash
umask
```

Example:

```text
0022
```

The actual default permissions depend on the program's requested base permissions and the umask.

A common conceptual model is:

```text
New file base permissions       666
New directory base permissions  777
```

The umask removes permission bits from these defaults.

For example, with a common umask of:

```text
022
```

new files commonly start as:

```text
644
```

and directories commonly start as:

```text
755
```

The exact resulting permissions can also depend on the application creating the file.

---

# 🔍 Checking Permissions

Use:

```bash
ls -l file.txt
```

For more detailed metadata:

```bash
stat file.txt
```

Example:

```bash
stat file.txt
```

This can show:

- Permissions
- Owner
- Group
- Size
- Timestamps
- Inode

---

# 🌍 Real-World DevOps Example

Suppose you have a deployment script:

```text
deploy.sh
```

Initially:

```text
-rw-r--r-- deploy.sh
```

Trying to execute it may fail because the execute permission is missing.

Add execute permission:

```bash
chmod u+x deploy.sh
```

Now:

```text
-rwxr--r-- deploy.sh
```

You can execute it:

```bash
./deploy.sh
```

This is a common situation when working with deployment scripts and CI/CD pipelines.

---

# 🐳 Docker and Permissions

Linux permissions are also important when working with containers.

For example, a container process may run as a non-root user.

If a mounted directory belongs to another UID/GID, the application may receive:

```text
Permission denied
```

Troubleshooting may involve checking:

```bash
ls -ln
```

The `-n` option displays numeric UID and GID values.

You may also inspect the running container's user configuration.

Understanding Linux ownership and permissions is therefore important for Docker and Kubernetes troubleshooting.

---

# ☸️ Kubernetes and Permissions

Permissions also matter in Kubernetes environments.

Containers may run as:

- Root
- Non-root users
- Specific UIDs
- Specific GIDs

Security contexts can control aspects of how containers run.

For example, Kubernetes can enforce non-root execution.

This connects Linux permissions directly with container security and DevSecOps.

---

# 🛠️ Hands-on Practice

Create a practice directory:

```bash
mkdir -p ~/permissions-lab
cd ~/permissions-lab
```

Create a file:

```bash
touch script.sh
```

Check permissions:

```bash
ls -l script.sh
```

Add execute permission:

```bash
chmod u+x script.sh
```

Check again:

```bash
ls -l script.sh
```

Set numeric permissions:

```bash
chmod 750 script.sh
```

Check:

```bash
ls -l script.sh
```

Create a directory:

```bash
mkdir shared
```

Set permissions:

```bash
chmod 750 shared
```

Check:

```bash
ls -ld shared
```

Check your umask:

```bash
umask
```

Check metadata:

```bash
stat script.sh
```

---

# 🧪 Practice Challenge

Create:

```text
permissions-lab/
├── scripts/
├── configs/
└── shared/
```

Then configure:

### `scripts/`

Owner:

```text
rwx
```

Group:

```text
r-x
```

Others:

```text
---
```

Use:

```bash
chmod 750 scripts
```

### Configuration file

Create:

```text
configs/app.conf
```

Set:

```text
Owner  → rw-
Group  → r--
Others → ---
```

Use:

```bash
chmod 640 configs/app.conf
```

### Shared directory

Create a shared directory and experiment with:

```bash
chmod g+s shared
```

Then inspect:

```bash
ls -ld shared
```

Finally, check your default permissions:

```bash
umask
```

---

# ⚠️ Permission Safety

Be careful with commands such as:

```bash
chmod -R
chown -R
```

Recursive permission or ownership changes can affect thousands of files.

Avoid blindly using:

```bash
chmod -R 777 /
```

or similar commands.

`777` gives read, write, and execute permissions to everyone and is usually an inappropriate solution to a permission problem.

Instead:

1. Identify the process/user.
2. Identify the required resource.
3. Check ownership.
4. Check current permissions.
5. Grant only the required access.

Follow the principle of:

> **Least Privilege**

---

# 💼 Interview Questions

- **What are the three basic Linux permissions?**  
  Read (`r`), Write (`w`), and Execute (`x`).

- **What are the three Linux permission classes?**  
  Owner, Group, and Others.

- **What does `chmod` do?**  
  `chmod` changes the permissions of files and directories.

- **What does `chown` do?**  
  `chown` changes the owner and optionally the group of a file or directory.

- **What does `chgrp` do?**  
  `chgrp` changes the group ownership of a file or directory.

- **What does permission `755` mean?**  
  The owner has `rwx`, while the group and others have `r-x`.

- **What does permission `644` mean?**  
  The owner has `rw-`, while the group and others have `r--`.

- **What does permission `777` mean?**  
  The owner, group, and others all have read, write, and execute permissions. It should generally be avoided unless there is a specific, justified requirement.

- **What does `rwx` represent?**  
  Read, write, and execute permissions.

- **What does execute permission mean for a directory?**  
  It allows a user to traverse/access entries within the directory.

- **What is SUID?**  
  SUID allows an executable to run with the privileges of its file owner.

- **What is SGID?**  
  SGID can cause an executable to run with the file's group privileges, and on directories it can cause newly created files to inherit the directory's group.

- **What is the sticky bit?**  
  The sticky bit is commonly used on shared directories to restrict users from deleting or renaming files owned by other users.

- **What is `umask`?**  
  `umask` specifies permission bits that are removed from the permissions requested when new files and directories are created.

- **What is the difference between `chmod` and `chown`?**  
  `chmod` changes permissions, while `chown` changes ownership.

- **How do you give execute permission to the owner of a script?**  
  Use:
  ```bash
  chmod u+x script.sh
  ```

- **How do you check file permissions?**  
  Use:
  ```bash
  ls -l filename
  ```
  or:
  ```bash
  stat filename
  ```

- **Why should `chmod -R 777` generally be avoided?**  
  It grants excessive permissions to everyone and can create serious security risks. Permissions should follow the principle of least privilege.

- **Why are Linux permissions important for DevOps?**  
  Permissions control access to application files, configuration, logs, deployment scripts, CI/CD environments, containers, and production infrastructure.

---

# 📚 Navigation

⬅️ Previous: **[10-Users-and-Groups.md](10-Users-and-Groups.md)**

➡️ Next: **[12-Processes-and-Services.md](12-Processes-and-Services.md)**

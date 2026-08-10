# 🖥️ Terminal Navigation


The Linux terminal is one of the most important tools for a DevOps Engineer.

Most Linux servers, cloud instances, containers, and CI/CD environments are managed primarily through the command line.

Terminal navigation means moving through directories, understanding your current location, viewing directory contents, and working with paths.

---

# 📌 What is a Linux Terminal?

A terminal is an interface through which you interact with a Linux system using commands.

Example:

```bash
ls
```

The terminal sends your command to the Shell, which interprets and executes it.

```text
User
  ↓
Terminal
  ↓
Shell
  ↓
Linux
```

---

# 📌 Current Working Directory

Linux always has a **current working directory**.

To see your current location, use:

```bash
pwd
```

`pwd` stands for:

**Print Working Directory**

Example:

```bash
$ pwd
/home/shubham
```

This tells you exactly where you are in the filesystem.

---

# 📂 Listing Directory Contents

Use:

```bash
ls
```

to list files and directories.

Example:

```bash
ls
```

### Detailed listing

```bash
ls -l
```

### Show hidden files

```bash
ls -a
```

### Detailed listing including hidden files

```bash
ls -la
```

### Human-readable file sizes

```bash
ls -lh
```

A commonly useful combination is:

```bash
ls -lah
```

---

# 📁 Changing Directories

Use:

```bash
cd
```

`cd` stands for **Change Directory**.

Example:

```bash
cd /var/log
```

Check your location:

```bash
pwd
```

---

# 🔙 Moving to the Parent Directory

Use:

```bash
cd ..
```

Example:

```text
/home/shubham/DevOps
```

Running:

```bash
cd ..
```

moves you to:

```text
/home/shubham
```

---

# 🏠 Going to Your Home Directory

You can use:

```bash
cd ~
```

or simply:

```bash
cd
```

The `~` symbol represents the current user's home directory.

Example:

```bash
cd ~
pwd
```

---

# ⬅️ Returning to the Previous Directory

Use:

```bash
cd -
```

Example:

```bash
cd /var/log
cd /etc
cd -
```

This takes you back to the previous working directory.

---

# 🛣️ Absolute Paths

An **absolute path** starts from the root directory `/`.

Example:

```text
/home/shubham/DevOps
```

You can navigate directly to it:

```bash
cd /home/shubham/DevOps
```

Absolute paths always describe the complete location from `/`.

---

# 📍 Relative Paths

A **relative path** starts from your current working directory.

Suppose you are currently in:

```text
/home/shubham
```

and there is a directory:

```text
/home/shubham/DevOps
```

You can use:

```bash
cd DevOps
```

instead of:

```bash
cd /home/shubham/DevOps
```

---

# 🔹 `.` and `..`

Linux provides special path references.

### `.`

Represents the current directory.

Example:

```bash
ls .
```

### `..`

Represents the parent directory.

Example:

```bash
ls ..
```

---

# 🌳 Path Navigation Example

Suppose the filesystem looks like:

```text
/home
└── shubham
    ├── DevOps
    │   ├── Linux
    │   └── Docker
    └── Projects
```

If you're here:

```text
/home/shubham
```

You can enter Linux using:

```bash
cd DevOps/Linux
```

Move back to DevOps:

```bash
cd ..
```

Move back to `/home/shubham`:

```bash
cd ../..
```

---

# 🔎 Finding Your Location

The most important command is:

```bash
pwd
```

Example:

```bash
$ pwd
/home/shubham/DevOps/Linux
```

Whenever you're unsure where you are, use `pwd`.

---

# 🧭 Useful Navigation Commands

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls` | List directory contents |
| `ls -l` | Detailed listing |
| `ls -a` | Show hidden files |
| `ls -lah` | Detailed human-readable listing |
| `cd directory` | Enter a directory |
| `cd ..` | Move to parent directory |
| `cd ~` | Go to home directory |
| `cd -` | Return to previous directory |
| `ls .` | List current directory |
| `ls ..` | List parent directory |

---

# 🔐 Hidden Files

Linux considers files and directories beginning with `.` as hidden.

Examples:

```text
.bashrc
.profile
.gitconfig
```

Normal `ls` does not show them.

Use:

```bash
ls -a
```

to view them.

Hidden does not mean secure or inaccessible. It simply means they are not shown by default.

---

# 📌 Understanding `ls -l`

Run:

```bash
ls -l
```

Example:

```text
drwxr-xr-x 2 shubham users 4096 Aug 10 projects
-rw-r--r-- 1 shubham users 1200 Aug 10 notes.txt
```

The output provides information such as:

```text
Permissions
    ↓
Owner
    ↓
Group
    ↓
Size
    ↓
Date
    ↓
Name
```

You will study permissions in detail later.

---

# 🌍 Real-World DevOps Example

Suppose you connect to an AWS Linux server using SSH:

```bash
ssh user@server
```

You need to locate an application's configuration file.

You might use:

```bash
pwd
```

then:

```bash
ls
```

then:

```bash
cd /etc
```

and:

```bash
ls
```

You may then navigate into the relevant configuration directory.

The ability to quickly navigate the filesystem is essential when troubleshooting production systems.

---

# 🛠️ Hands-on Practice

Try the following commands in your Linux environment:

```bash
pwd
```

```bash
ls
```

```bash
ls -lah
```

```bash
cd /tmp
```

```bash
pwd
```

```bash
cd ..
```

```bash
pwd
```

```bash
cd ~
```

```bash
pwd
```

Then practice:

```bash
cd /var/log
```

```bash
pwd
```

```bash
cd -
```

```bash
pwd
```

---

# 🧪 Practice Challenge

Without copying commands from the previous section:

1. Go to your home directory.
2. Create the following path mentally:

```text
DevOps/Linux/Practice
```

3. Navigate through the path using relative paths.
4. Move back one directory using `..`.
5. Return to your home directory using `~`.
6. Navigate to `/var/log`.
7. Return to your previous directory using `cd -`.
8. Use `pwd` after each major movement.

The goal is to become comfortable navigating without using a graphical file manager.

---

# 💼 Interview Questions

- **What is the purpose of `pwd`?**  
  `pwd` displays the absolute path of the current working directory.

- **What does `cd` do?**  
  `cd` changes the current working directory.

- **What is the difference between an absolute path and a relative path?**  
  An absolute path starts from `/` and specifies the complete location. A relative path starts from the current working directory.

- **What does `.` represent in Linux?**  
  `.` represents the current directory.

- **What does `..` represent?**  
  `..` represents the parent directory.

- **What does `~` represent?**  
  `~` represents the current user's home directory.

- **What does `cd -` do?**  
  `cd -` changes to the previous working directory.

- **How do you display hidden files?**  
  Use `ls -a`.

- **How do you display detailed information about files?**  
  Use `ls -l`.

- **How do you display file sizes in a human-readable format?**  
  Use `ls -lh`.

- **What is the difference between `ls` and `ls -la`?**  
  `ls` displays normal directory contents, while `ls -la` displays detailed information including hidden files.

- **Why is terminal navigation important for DevOps Engineers?**  
  DevOps engineers frequently manage remote Linux servers, containers, cloud instances, and CI/CD environments through the command line, making efficient terminal navigation an essential skill.

---

# 📚 Navigation

⬅️ Previous: **[05-Filesystem-Hierarchy-Standard.md](05-Filesystem-Hierarchy-Standard.md)**

➡️ Next: **[07-Essential-Linux-Commands.md](07-Essential-Linux-Commands.md)**

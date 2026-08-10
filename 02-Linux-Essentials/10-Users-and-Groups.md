# 👤 Linux Users and Groups


Linux is a multi-user operating system. Multiple users can access the same Linux system while having different permissions, files, processes, and levels of access.

**Users and Groups** are fundamental to Linux security and administration.

As a DevOps Engineer, you will work with users and groups when:

- Managing Linux servers
- Configuring SSH access
- Setting file ownership
- Managing application services
- Configuring permissions
- Running CI/CD jobs
- Deploying applications
- Troubleshooting access issues

---

# 📌 What is a User?

A **user** represents an identity that can interact with a Linux system.

Each user has information such as:

- Username
- User ID (UID)
- Primary group
- Secondary groups
- Home directory
- Login shell

You can see your current user with:

```bash
whoami
```

View detailed information:

```bash
id
```

Example:

```text
uid=1000(shubham) gid=1000(shubham) groups=1000(shubham),27(sudo)
```

---

# 🆔 User ID (UID)

Every Linux user has a numeric **UID**.

Example:

```text
shubham → UID 1000
```

Linux uses the UID internally to identify the user.

The username is mainly a human-friendly representation of the UID.

You can check your UID with:

```bash
id -u
```

---

# 👥 What is a Group?

A **group** is a collection of users.

Groups make it easier to manage permissions for multiple users.

For example:

```text
devops
├── shubham
├── rahul
└── amit
```

Instead of assigning permissions individually to every user, you can assign permissions to the `devops` group.

---

# 🆔 Group ID (GID)

Every Linux group has a numeric **Group ID (GID)**.

You can view your group information using:

```bash
id
```

Example:

```text
gid=1000(devops)
```

---

# 🔑 Primary Group

Every Linux user has a **primary group**.

It is the default group associated with the user.

You can check it using:

```bash
id username
```

Example:

```bash
id shubham
```

---

# ➕ Secondary Groups

A user can also belong to additional groups.

For example:

```text
User: shubham

Primary Group:
devops

Secondary Groups:
docker
sudo
developers
```

Secondary groups are useful for granting additional access without changing the user's primary group.

Check all groups:

```bash
groups
```

Or:

```bash
id
```

---

# 📁 User and Group Information Files

Linux stores local user and group information in several important files.

## `/etc/passwd`

Contains information about local user accounts.

View it with:

```bash
cat /etc/passwd
```

A typical entry looks like:

```text
shubham:x:1000:1000:Shubham:/home/shubham:/bin/bash
```

The fields represent:

```text
Username
Password placeholder
UID
GID
GECOS / User information
Home directory
Login shell
```

---

# 🔐 `/etc/shadow`

Contains password hashes and password-aging information for local accounts.

```bash
sudo cat /etc/shadow
```

Access to this file is restricted because it contains sensitive authentication information.

You generally should **not edit `/etc/shadow` manually**.

---

# 👥 `/etc/group`

Contains local group information.

View it using:

```bash
cat /etc/group
```

Example:

```text
devops:x:1001:shubham,rahul
```

The entry identifies:

- Group name
- Group ID
- Members

---

# 🔑 `/etc/gshadow`

Contains secure group information such as group passwords and membership administration data.

It is normally protected from regular users.

```bash
sudo cat /etc/gshadow
```

---

# ➕ Creating Users

## `useradd`

Creates a user account.

Example:

```bash
sudo useradd shubham
```

Create a user with a home directory:

```bash
sudo useradd -m shubham
```

Specify a login shell:

```bash
sudo useradd -m -s /bin/bash shubham
```

---

# 🔐 Setting a Password

Use:

```bash
sudo passwd shubham
```

You will be prompted to enter the password.

For security, avoid placing plaintext passwords directly in shell commands or scripts.

---

# 👀 Viewing User Information

## `id`

```bash
id shubham
```

## `getent`

`getent` queries configured system databases.

For example:

```bash
getent passwd shubham
```

Query a group:

```bash
getent group devops
```

This is useful because user and group information may come from sources beyond local files, such as LDAP or other identity services.

---

# 📋 Listing Users

A simple way to view local users is:

```bash
cat /etc/passwd
```

To display only usernames:

```bash
cut -d: -f1 /etc/passwd
```

However, remember that enterprise Linux systems may use centralized identity services, so `/etc/passwd` alone may not represent every user known to the system.

---

# 👥 Creating Groups

Use:

```bash
sudo groupadd devops
```

Check the group:

```bash
getent group devops
```

---

# ➕ Adding a User to a Group

On many Linux distributions:

```bash
sudo usermod -aG devops shubham
```

Important:

```text
-a → Append
-G → Supplementary groups
```

The `-a` option is important.

Without it, you can accidentally replace the user's existing supplementary group memberships.

---

# 🔍 Checking Group Membership

Use:

```bash
groups shubham
```

or:

```bash
id shubham
```

---

# ➖ Removing a User from a Group

On systems using GNU `usermod`, you can use:

```bash
sudo gpasswd -d shubham devops
```

Then verify:

```bash
groups shubham
```

---

# 🔄 Changing a User's Primary Group

Use:

```bash
sudo usermod -g devops shubham
```

Verify:

```bash
id shubham
```

Be careful when changing primary groups because files and applications may depend on existing ownership and group configuration.

---

# 🏠 User Home Directories

A typical user has a home directory:

```text
/home/shubham
```

You can find the home directory using:

```bash
echo $HOME
```

or:

```bash
getent passwd shubham
```

---

# 🐚 Login Shell

A user's login shell determines which shell is started for interactive login sessions.

Example:

```text
/bin/bash
```

Check it with:

```bash
getent passwd shubham
```

You can also inspect the current shell:

```bash
echo $SHELL
```

---

# 🔄 Changing a User's Shell

Use:

```bash
sudo usermod -s /bin/bash shubham
```

Check:

```bash
getent passwd shubham
```

Available shells can often be found in:

```bash
cat /etc/shells
```

---

# 🔒 Locking a User Account

A user account can be locked when interactive login should be disabled.

Example:

```bash
sudo usermod -L shubham
```

Unlock:

```bash
sudo usermod -U shubham
```

The exact authentication behavior can depend on the system's authentication configuration.

---

# 🗑️ Deleting Users

Remove a user:

```bash
sudo userdel shubham
```

Remove the user and their home directory:

```bash
sudo userdel -r shubham
```

Be careful when deleting users because files owned by that UID may remain elsewhere on the system.

---

# 🗑️ Deleting Groups

Remove a group:

```bash
sudo groupdel devops
```

Make sure the group is no longer required before deleting it.

---

# 👑 Root User

The **root user** is the superuser on Linux.

Root has extensive privileges over the system.

The root user can generally:

- Install software
- Modify system configuration
- Manage users
- Manage services
- Change permissions
- Access protected files
- Shut down the system

Because root has extensive privileges, it should be used carefully.

---

# 🛡️ `sudo`

`sudo` allows an authorized user to execute a command with elevated privileges according to the system's sudo policy.

Example:

```bash
sudo apt update
```

Instead of logging in directly as root, administrators commonly use `sudo` for individual privileged operations.

This provides better accountability and reduces unnecessary use of a root shell.

---

# 📜 Sudo Configuration

The main sudo configuration file is:

```text
/etc/sudoers
```

You should generally edit sudo configuration using:

```bash
sudo visudo
```

`visudo` validates the syntax before saving the configuration, reducing the risk of breaking sudo access.

---

# 🔐 Users, Groups, and Permissions

Users and groups become especially important when managing file permissions.

For example:

```text
-rwxr-x---
```

This can be understood as:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

If an application directory belongs to the `devops` group, you can grant access to multiple users through group membership.

Permissions will be covered in detail in the upcoming Linux Permissions section.

---

# 🌍 Real-World DevOps Example

Imagine a company has a production server:

```text
Linux Server
│
├── developers
│
├── devops
│
├── monitoring
│
└── deployment
```

Instead of giving every user unrestricted access, administrators can create groups:

```text
developers
devops
monitoring
deployment
```

Then permissions can be assigned based on responsibilities.

For example:

```text
Application Directory
        │
        └── Group: devops
```

Only members of the appropriate group receive the required access.

This follows the principle of:

> **Give users only the access they need to perform their job.**

---

# ☁️ DevOps Example: CI/CD User

A CI/CD system may use a dedicated service account to perform deployment tasks.

For example:

```text
deployment-user
       │
       ├── SSH access
       ├── Application deployment permissions
       └── Limited system privileges
```

Instead of using the root account for automation, organizations generally prefer dedicated identities with narrowly scoped permissions.

---

# 🧪 Hands-on Practice

Create a test group:

```bash
sudo groupadd devops
```

Create a test user:

```bash
sudo useradd -m -s /bin/bash devuser
```

Set a password:

```bash
sudo passwd devuser
```

Add the user to the group:

```bash
sudo usermod -aG devops devuser
```

Check the user:

```bash
id devuser
```

Check the group:

```bash
getent group devops
```

Check the user's home directory:

```bash
getent passwd devuser
```

Check the user's shell:

```bash
getent passwd devuser
```

Remove the user from the group:

```bash
sudo gpasswd -d devuser devops
```

Verify:

```bash
groups devuser
```

After completing the lab, clean up the test account if it is no longer needed:

```bash
sudo userdel -r devuser
```

And remove the test group:

```bash
sudo groupdel devops
```

---

# 🧪 Practice Challenge

Create a small Linux user-management scenario.

### Requirement

Create:

```text
Group:
developers

Users:
developer1
developer2
```

Then:

1. Create the `developers` group.
2. Create both users with home directories.
3. Set passwords.
4. Add both users to the `developers` group.
5. Verify their UIDs.
6. Verify their primary and supplementary groups.
7. Check their home directories.
8. Check their login shells.
9. Remove `developer2` from the group.
10. Verify the change.
11. Clean up the test users and group.

Use:

```bash
id
```

```bash
groups
```

```bash
getent passwd
```

```bash
getent group
```

to verify your work.

---

# ⚠️ Important Safety Practices

User management affects system access, so be careful when working on production servers.

Before deleting or modifying an account:

```bash
id username
```

Check whether the account is being used.

Avoid:

- Sharing root credentials
- Giving unnecessary sudo access
- Using root for routine work
- Storing passwords in scripts
- Deleting users without checking their files
- Overwriting supplementary groups accidentally

Remember:

```bash
usermod -aG group user
```

The `-a` prevents existing supplementary group memberships from being replaced.

---

# 💼 Interview Questions

- **What is a user in Linux?**  
  A user represents an identity that can interact with the Linux system and is associated with a UID, groups, home directory, and login shell.

- **What is a UID?**  
  UID stands for User ID. It is the numeric identifier Linux uses internally to identify a user.

- **What is a group in Linux?**  
  A group is a collection of users that allows permissions and access to be managed for multiple users.

- **What is a GID?**  
  GID stands for Group ID. It is the numeric identifier assigned to a Linux group.

- **What is the difference between a primary group and a supplementary group?**  
  A user has one primary group, while they can belong to multiple supplementary groups for additional access.

- **What is `/etc/passwd`?**  
  `/etc/passwd` contains account information for local users, including usernames, UIDs, GIDs, home directories, and login shells.

- **What is `/etc/shadow`?**  
  `/etc/shadow` stores password hashes and password-aging information for local accounts and is restricted to privileged access.

- **What is `/etc/group`?**  
  `/etc/group` contains information about local groups and their memberships.

- **What is the root user?**  
  Root is the Linux superuser with extensive privileges over the system.

- **What is `sudo`?**  
  `sudo` allows an authorized user to execute commands with elevated privileges according to the configured sudo policy.

- **How do you create a user?**  
  A common command is:
  ```bash
  sudo useradd -m username
  ```

- **How do you create a group?**  
  Use:
  ```bash
  sudo groupadd groupname
  ```

- **How do you add a user to a supplementary group?**  
  Use:
  ```bash
  sudo usermod -aG groupname username
  ```

- **Why is `-a` important in `usermod -aG`?**  
  `-a` means append. It prevents the user's existing supplementary group memberships from being replaced.

- **How do you check a user's groups?**  
  Use:
  ```bash
  id username
  ```
  or:
  ```bash
  groups username
  ```

- **How do you check information about a user from the system's configured identity sources?**  
  Use:
  ```bash
  getent passwd username
  ```

- **Why should DevOps engineers understand users and groups?**  
  Users and groups are fundamental to Linux access control. They are used for SSH access, application services, CI/CD automation, file ownership, and secure infrastructure management.

---

# 📚 Navigation

⬅️ Previous: **[09-File-Management.md](09-File-Management.md)**

➡️ Next: **[11-Permissions.md](11-Permissions.md)**

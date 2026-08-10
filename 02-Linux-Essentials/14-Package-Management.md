# 📦 Linux Package Management

Package management is the process of installing, updating, removing, and maintaining software on a Linux system.

As a DevOps Engineer, you will regularly use package managers to:

- Install software
- Update system packages
- Remove unwanted packages
- Fix dependencies
- Search for software
- Check installed versions
- Automate server setup
- Build deployment environments

Common Linux package management tools include:

- `apt`
- `dnf`
- `yum`
- `snap`

---

# 📌 What is a Package?

A package is a collection of files required to install and run a piece of software.

A package may contain:

- Application binaries
- Libraries
- Configuration files
- Documentation
- Metadata
- Dependency information

Examples:

```text
nginx
git
curl
python3
docker
```

---

# 📌 What is a Package Manager?

A package manager automates the process of managing software packages.

Instead of manually downloading and installing every dependency, a package manager can:

```text
Search
  ↓
Download
  ↓
Resolve Dependencies
  ↓
Install
  ↓
Configure
  ↓
Update
  ↓
Remove
```

---

# 🐧 Linux Package Management Ecosystem

Different Linux distributions use different package management systems.

| Distribution Family | Package Format | Common Package Manager |
|---|---|---|
| Debian / Ubuntu | `.deb` | `apt` |
| RHEL / Fedora | `.rpm` | `dnf` |
| Older RHEL-based systems | `.rpm` | `yum` |
| Universal application packaging | Snap | `snap` |

The exact commands available depend on the Linux distribution.

---

# 🟢 APT

`apt` is the high-level package management command commonly used on Debian and Ubuntu systems.

Examples:

```bash
apt update
apt install
apt remove
apt upgrade
```

On systems where administrator privileges are required:

```bash
sudo apt ...
```

---

# 🔄 `apt update`

Updates the local package index.

```bash
sudo apt update
```

Important:

```text
apt update
```

does **not** upgrade installed packages.

It refreshes information about available packages and versions.

Conceptually:

```text
Repositories
     ↓
Package Metadata
     ↓
Local Package Index
```

---

# ⬆️ `apt upgrade`

Upgrades installed packages to newer available versions.

```bash
sudo apt upgrade
```

A common workflow is:

```bash
sudo apt update
sudo apt upgrade
```

---

# 📥 Installing Packages with APT

Install a package:

```bash
sudo apt install nginx
```

Install multiple packages:

```bash
sudo apt install git curl wget
```

---

# 🔍 Searching for Packages

Search the package index:

```bash
apt search nginx
```

Show package information:

```bash
apt show nginx
```

---

# 📋 Listing Installed Packages

You can use:

```bash
apt list --installed
```

You can also query the lower-level Debian package database:

```bash
dpkg -l
```

---

# 🗑️ Removing Packages

Remove a package:

```bash
sudo apt remove nginx
```

Remove a package and its system configuration files where supported:

```bash
sudo apt purge nginx
```

Remove packages that are no longer required:

```bash
sudo apt autoremove
```

Be careful when removing packages because other software may depend on them.

---

# 🧹 APT Cache

APT stores downloaded package files in its local cache.

You can inspect cache usage with:

```bash
du -sh /var/cache/apt/archives
```

Clean downloaded package files:

```bash
sudo apt clean
```

Remove only package files that can no longer be downloaded:

```bash
sudo apt autoclean
```

---

# 🟠 DNF

`dnf` is a modern package manager used by Fedora and modern RHEL-based systems.

Examples:

```bash
sudo dnf install nginx
```

Update packages:

```bash
sudo dnf upgrade
```

Remove a package:

```bash
sudo dnf remove nginx
```

---

# 🔍 Searching with DNF

Search for packages:

```bash
dnf search nginx
```

Show package information:

```bash
dnf info nginx
```

List installed packages:

```bash
dnf list installed
```

---

# 📥 Installing Packages with DNF

Example:

```bash
sudo dnf install git
```

Install multiple packages:

```bash
sudo dnf install git curl wget
```

---

# ⬆️ Updating with DNF

Update installed packages:

```bash
sudo dnf upgrade
```

You can also use:

```bash
sudo dnf update
```

On modern DNF systems, `update` and `upgrade` generally perform the same package update operation.

---

# 🗑️ Removing Packages with DNF

Remove a package:

```bash
sudo dnf remove nginx
```

Clean unused dependencies when appropriate:

```bash
sudo dnf autoremove
```

---

# 🟡 YUM

`yum` is the traditional package manager used by older Red Hat-based distributions.

Example:

```bash
sudo yum install nginx
```

Update packages:

```bash
sudo yum update
```

Remove packages:

```bash
sudo yum remove nginx
```

Search:

```bash
yum search nginx
```

---

# 🔄 YUM and DNF

Modern RHEL-based systems use DNF.

On many current systems:

```text
yum
  ↓
dnf compatibility interface
```

However, you may still encounter `yum` in:

- Older servers
- Legacy documentation
- Existing automation scripts
- Older RHEL/CentOS environments

As a DevOps Engineer, you should understand both.

---

# 🟣 Snap

Snap is a packaging and software distribution system developed by Canonical.

Snap packages are designed to bundle applications and their dependencies in a way that can work across different Linux distributions that support Snap.

---

# 📥 Installing Snap Packages

Example:

```bash
sudo snap install hello-world
```

---

# 🔍 Searching Snap Packages

```bash
snap find nginx
```

---

# 📋 Listing Installed Snap Packages

```bash
snap list
```

---

# 🔄 Updating Snap Packages

Refresh available Snap updates:

```bash
sudo snap refresh
```

---

# 🗑️ Removing a Snap Package

```bash
sudo snap remove hello-world
```

---

# 📊 APT vs DNF vs YUM vs Snap

| Tool | Commonly Used With | Package / Model |
|---|---|---|
| `apt` | Debian / Ubuntu | `.deb` |
| `dnf` | Fedora / RHEL | `.rpm` |
| `yum` | Older RHEL-based systems | `.rpm` |
| `snap` | Linux distributions supporting Snap | Snap package |

---

# 📦 Package Repositories

Package managers usually obtain software from configured repositories.

Conceptually:

```text
Linux Server
     ↓
Package Manager
     ↓
Repository
     ↓
Package
     ↓
Dependencies
     ↓
Installation
```

Repositories provide:

- Packages
- Package metadata
- Versions
- Dependencies
- Updates
- Security fixes

---

# 🔗 Dependencies

Software packages often depend on other packages.

For example:

```text
Application
    ↓
Library A
    ↓
Library B
    ↓
Library C
```

A package manager resolves these dependencies automatically.

This is one of the biggest advantages of using a package manager instead of manually installing software.

---

# 🔐 Package Security

Package managers can use repository metadata and cryptographic signatures to help verify package authenticity and integrity.

For example, APT repositories use signed metadata, while RPM-based systems use package signing mechanisms.

Always prefer trusted repositories.

Avoid installing unknown packages from untrusted sources on production systems.

---

# 🔢 Checking Installed Software Versions

Check a package using APT:

```bash
apt policy nginx
```

For DNF:

```bash
dnf info nginx
```

For the actual executable:

```bash
nginx -v
```

For Git:

```bash
git --version
```

For Python:

```bash
python3 --version
```

---

# 📜 Package Files vs Executables

A package manager manages the software package, while the installed application provides executable commands.

For example:

```text
Package:
nginx

Executable:
nginx

Configuration:
Usually under /etc

Logs:
Often under /var/log
```

The exact locations depend on the software and distribution.

---

# 🔎 Finding Which Package Provides a File

On Debian/Ubuntu systems, tools such as:

```bash
apt-file
```

can be used to search package contents when configured.

For installed packages, `dpkg -S` can identify which package owns a file:

```bash
dpkg -S /usr/bin/curl
```

On RPM-based systems:

```bash
rpm -qf /usr/bin/curl
```

---

# 🧰 Lower-Level Package Tools

High-level package managers use lower-level package tools underneath.

### Debian-based systems

```text
apt
 ↓
dpkg
```

`dpkg` works directly with `.deb` packages.

Examples:

```bash
dpkg -l
```

```bash
dpkg -i package.deb
```

### RPM-based systems

```text
dnf / yum
 ↓
rpm
```

`rpm` works directly with `.rpm` packages.

Example:

```bash
rpm -qa
```

---

# 🆚 APT vs DPKG

| APT | DPKG |
|---|---|
| High-level package manager | Low-level package tool |
| Resolves dependencies | Works directly with `.deb` packages |
| Uses repositories | Can install local `.deb` packages |
| Easier for normal administration | Useful for package-level operations |

Example:

```bash
sudo apt install nginx
```

versus:

```bash
sudo dpkg -i package.deb
```

APT is generally preferred for normal package installation because it handles dependencies.

---

# 🆚 DNF/YUM vs RPM

| DNF/YUM | RPM |
|---|---|
| High-level package management | Low-level package management |
| Handles dependencies | Works directly with RPM packages |
| Uses repositories | Installs/query RPM packages |
| Common for system administration | Useful for package-level operations |

---

# 🛠️ Package Management in DevOps

Package management is often part of server provisioning.

For example:

```text
New Linux Server
       ↓
Update Package Index
       ↓
Install Git
       ↓
Install Python
       ↓
Install Docker
       ↓
Install Monitoring Agent
       ↓
Configure Services
       ↓
Deploy Application
```

This process can be automated using:

- Bash
- Ansible
- Cloud-init
- Terraform provisioning
- Configuration management tools
- CI/CD pipelines

---

# ☁️ Cloud Server Example

Suppose you launch an Ubuntu EC2 instance.

You might connect through SSH:

```bash
ssh user@server
```

Then install required software:

```bash
sudo apt update
sudo apt install git curl nginx
```

Start the web server:

```bash
sudo systemctl enable --now nginx
```

Test it:

```bash
curl http://localhost
```

This combines:

```text
Package Management
        ↓
Service Management
        ↓
Application Testing
```

---

# 🤖 Automation Example

Instead of manually running:

```bash
sudo apt update
sudo apt install git curl nginx
```

you could automate the process with configuration management.

For example, Ansible can declare the desired package state:

```yaml
- name: Install required packages
  ansible.builtin.apt:
    name:
      - git
      - curl
      - nginx
    state: present
    update_cache: true
```

This will become important when you reach the **Ansible / Configuration Management** phase.

---

# 🧪 Hands-on Practice — Ubuntu/Debian

If you are using Ubuntu, practice:

```bash
sudo apt update
```

Search for a package:

```bash
apt search nginx
```

View package information:

```bash
apt show nginx
```

Install:

```bash
sudo apt install nginx
```

Check:

```bash
nginx -v
```

Check the service:

```bash
systemctl status nginx
```

Remove:

```bash
sudo apt remove nginx
```

---

# 🧪 Hands-on Practice — RHEL/Fedora

If you have access to a Fedora/RHEL-based system:

```bash
sudo dnf search nginx
```

View information:

```bash
dnf info nginx
```

Install:

```bash
sudo dnf install nginx
```

Check:

```bash
rpm -q nginx
```

Remove:

```bash
sudo dnf remove nginx
```

---

# 🧪 Practice Challenge

On your Linux environment:

### Step 1

Identify your distribution:

```bash
cat /etc/os-release
```

### Step 2

Identify the appropriate package manager.

### Step 3

Search for:

```text
curl
git
nginx
```

### Step 4

Choose a safe package and inspect its information.

### Step 5

Install it.

### Step 6

Verify the installed version.

### Step 7

Check whether it created a service.

### Step 8

Remove the package if you no longer need it.

Document:

```text
Distribution:
Package Manager:
Package:
Version:
Installation Command:
Verification Command:
Removal Command:
```

---

# 🌍 Real-World DevOps Example

A production Linux server needs:

```text
Git
Python
Nginx
Monitoring Agent
Docker
```

Instead of manually downloading software from random websites, the DevOps engineer uses the distribution's trusted package repositories whenever appropriate.

The workflow becomes:

```text
Repository
    ↓
Package Manager
    ↓
Dependencies
    ↓
Installation
    ↓
Configuration
    ↓
Service
    ↓
Monitoring
```

This provides a repeatable and maintainable approach to server administration.

---

# ⚠️ Package Management Safety

Avoid blindly running commands copied from the internet.

Before installing software:

1. Check the package name.
2. Check the repository.
3. Check the package version.
4. Understand dependencies.
5. Confirm the package is trusted.

Be especially careful with:

```bash
sudo apt remove
sudo dnf remove
sudo yum remove
```

Removing a package can also affect dependent software.

On production systems, test package upgrades before applying them broadly.

---

# 💼 Interview Questions

- **What is a package manager?**  
  A package manager is a tool used to install, update, remove, and manage software packages and their dependencies.

- **What is a package?**  
  A package is a collection of software files and metadata required to install and manage an application or component.

- **What is APT?**  
  APT is the high-level package management system commonly used on Debian and Ubuntu systems.

- **What is DNF?**  
  DNF is a modern package manager used by Fedora and modern RHEL-based systems.

- **What is YUM?**  
  YUM is the traditional package manager used by older Red Hat-based systems. On many modern systems, it is implemented as a compatibility interface to DNF.

- **What is Snap?**  
  Snap is a software packaging and distribution system that packages applications in a format designed to work across supported Linux distributions.

- **What is the difference between `apt update` and `apt upgrade`?**  
  `apt update` refreshes the local package index, while `apt upgrade` upgrades installed packages to newer available versions.

- **How do you install a package using APT?**  
  Use:
  ```bash
  sudo apt install package-name
  ```

- **How do you install a package using DNF?**  
  Use:
  ```bash
  sudo dnf install package-name
  ```

- **How do you remove a package using APT?**  
  Use:
  ```bash
  sudo apt remove package-name
  ```

- **How do you search for a package using APT?**  
  Use:
  ```bash
  apt search package-name
  ```

- **How do you search for a package using DNF?**  
  Use:
  ```bash
  dnf search package-name
  ```

- **What is the difference between APT and DPKG?**  
  APT is a high-level package manager that handles repositories and dependencies, while DPKG works directly with Debian `.deb` packages.

- **What is the difference between DNF and RPM?**  
  DNF is a high-level package manager that handles repositories and dependencies, while RPM works directly with `.rpm` packages.

- **Why are package repositories important?**  
  Repositories provide trusted packages, metadata, versions, dependencies, and updates that package managers can use to install and maintain software.

- **What are package dependencies?**  
  Dependencies are other software packages or libraries required for an application to function correctly.

- **How would you check which package owns a file on Ubuntu/Debian?**  
  For an installed file, use:
  ```bash
  dpkg -S /path/to/file
  ```

- **How would you check which RPM package owns a file?**  
  Use:
  ```bash
  rpm -qf /path/to/file
  ```

- **Why is package management important in DevOps?**  
  Package management allows DevOps engineers to consistently install, update, and maintain software on servers and automate environment provisioning.

- **How can package management be automated?**  
  It can be automated using Bash, Ansible, cloud-init, configuration management, provisioning scripts, and CI/CD pipelines.

---

# 📚 Navigation

⬅️ Previous: **[13-Storage.md](13-Storage.md)**

➡️ Next: **[15-Shell.md](15-Shell.md)**

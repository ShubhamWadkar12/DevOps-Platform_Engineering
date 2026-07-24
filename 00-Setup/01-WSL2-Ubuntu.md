# WSL2 (Windows Subsystem for Linux)

## 📖 Overview

Windows Subsystem for Linux (WSL) is a feature in Microsoft Windows that allows you to run a real Linux environment directly on Windows without creating a virtual machine or using dual boot.

It enables developers, DevOps engineers, and system administrators to use Linux tools, commands, and applications while continuing to work on Windows.

In this roadmap, Ubuntu running on WSL2 will be our primary operating system for learning Linux, Docker, Kubernetes, Git, Python, Terraform, and many other DevOps tools.

---

# 🎯 Learning Objectives

After completing this chapter, you will understand:

- What WSL is
- Why WSL was created
- Difference between WSL1 and WSL2
- Why Ubuntu is used
- Why DevOps engineers prefer WSL
- How WSL works internally
- Installation and verification
- Basic WSL commands

---

# What is WSL?

WSL stands for **Windows Subsystem for Linux**.

It allows Linux distributions like Ubuntu to run directly inside Windows.

This means you can execute Linux commands, run shell scripts, install packages, use SSH, Docker, Python, Git, Kubernetes tools, and many other Linux-based utilities without leaving Windows.

Unlike traditional virtual machines, WSL is tightly integrated with Windows, making it lightweight and fast.

---

# Why was WSL Created?

Before WSL, Windows users had three main options:

- Install Linux using Dual Boot
- Use a Virtual Machine (VirtualBox or VMware)
- Rent a Linux server

Each option had disadvantages:

### Dual Boot

- Restart required every time
- Disk partitioning
- Less convenient

### Virtual Machine

- High RAM usage
- High CPU usage
- Slower performance
- Additional configuration

Microsoft introduced WSL to provide a simple and efficient way to use Linux alongside Windows.

---

# What is WSL2?

WSL has two versions:

- WSL1
- WSL2

WSL2 is the latest version and is the recommended choice for modern development.

Unlike WSL1, WSL2 runs a real Linux kernel provided by Microsoft.

This improves compatibility, performance, and support for modern tools such as Docker and Kubernetes.

---

# WSL1 vs WSL2

| Feature | WSL1 | WSL2 |
|----------|------|------|
| Linux Kernel | No | Yes |
| Performance | Good | Excellent |
| Docker Support | Limited | Full |
| Kubernetes Support | Limited | Full |
| File Compatibility | Partial | Full |
| Recommended | ❌ No | ✅ Yes |

---

# Why Ubuntu?

Ubuntu is one of the most popular Linux distributions.

Many companies use Ubuntu for:

- Development
- Cloud Servers
- DevOps
- Containers
- Automation
- CI/CD

Ubuntu has:

- Excellent documentation
- Large community
- Long Term Support (LTS)
- Easy package management
- Wide software compatibility

For beginners, Ubuntu is one of the easiest Linux distributions to learn.

---

# Why DevOps Engineers Use WSL

A DevOps engineer works with Linux every day.

Examples include:

- Managing servers
- Running Docker
- Working with Kubernetes
- Writing Bash scripts
- Using Git
- Automating deployments
- Configuring cloud resources

WSL allows all of this directly from a Windows machine without needing a separate Linux computer.

---

# How WSL Works

The workflow is simple:

```
Windows
      │
      ▼
Windows Subsystem for Linux (WSL2)
      │
      ▼
Linux Kernel
      │
      ▼
Ubuntu Distribution
      │
      ▼
Linux Commands & Applications
```

When you open Ubuntu from Windows, you are working inside a genuine Linux environment while still having access to your Windows files if needed.

---

# Installation

Install WSL using PowerShell (Run as Administrator):

```powershell
wsl --install
```

Restart the computer if prompted.

---

## Install Ubuntu

```powershell
wsl --install -d Ubuntu   (-d tells which distribution to be used)
```

---

## Check Installed Distributions

```powershell
wsl --list
```

or

```powershell
wsl -l
```

---

## Check WSL Version

```powershell
wsl --status
```

---

## Check Distribution Version

```powershell
wsl -l -v
```

---

# Update Ubuntu

```bash
sudo apt update              (download)  
sudo apt upgrade -y          (install)
```

---

# Verify Installation

Check Linux version:

```bash
uname -a
```

Check Ubuntu version:

```bash
lsb_release -a
```

Check current user:

```bash
whoami
```

Check current directory:

```bash
pwd
```

---

# Advantages of WSL2

- Lightweight
- Fast startup
- Real Linux kernel
- Docker support
- Kubernetes support
- Easy file sharing with Windows
- No dual boot
- No virtual machine management
- Excellent development experience

---

# Limitations

- Not intended to replace production Linux servers.
- Some low-level hardware features behave differently than on a native Linux installation.
- GUI applications are supported, but most DevOps work is done from the terminal.

---

# Best Practices

- Always use Ubuntu LTS.
- Keep Ubuntu updated.
- Use WSL2 instead of WSL1.
- Store Linux project files inside the Linux filesystem (`~/`) for the best performance.
- Use VS Code with the Remote - WSL extension.
- Learn Linux commands instead of relying on graphical tools.

---

# Interview Questions

- **What is WSL?**
  > WSL (Windows Subsystem for Linux) lets you run a Linux environment directly on Windows without a virtual machine.
- **Why is WSL useful for DevOps?**
  > It provides a Linux environment to use DevOps tools like Docker, Git, Kubernetes, Terraform, and Ansible on Windows.
- **Difference between WSL1 and WSL2?**
  > WSL1 translates Linux system calls, while WSL2 runs a real Linux kernel with better compatibility and performance.
- **Why is Ubuntu commonly used?**
  > Ubuntu is stable, beginner-friendly, well-documented, and widely supported in the DevOps ecosystem.
- **Why is WSL2 preferred over VirtualBox?**
  > WSL2 is lighter, faster, consumes fewer resources, and integrates seamlessly with Windows.
- **Can Docker run on WSL2?**
  > Yes, Docker Desktop uses WSL2 as its backend to run Linux containers efficiently.
- **Does WSL use a real Linux kernel?**
  > Yes, WSL2 uses a real Microsoft-maintained Linux kernel.
- **Why do companies prefer Linux for servers?**
  > Linux is secure, stable, high-performance, open-source, and ideal for server and cloud environments.

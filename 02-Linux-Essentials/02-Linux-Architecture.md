# 🏗️ Linux Architecture


Linux follows a layered architecture that allows users, applications, and hardware to communicate in a secure and organized way.

For a DevOps Engineer, understanding Linux Architecture is important because tools such as Docker, Kubernetes, Git, Ansible, and CI/CD systems commonly run on Linux.

---

# 📌 What is Linux Architecture?

Linux Architecture describes how the different components of a Linux system work together.

A simplified view is:

```text
+--------------------------------------+
|              User                    |
+--------------------------------------+
                 │
                 ▼
+--------------------------------------+
|       Applications / Programs        |
| Docker • Git • Python • NGINX        |
+--------------------------------------+
                 │
                 ▼
+--------------------------------------+
|          Shell / CLI                 |
|       Bash • Zsh • Fish              |
+--------------------------------------+
                 │
                 ▼
+--------------------------------------+
|           Linux Kernel               |
+--------------------------------------+
                 │
                 ▼
+--------------------------------------+
|             Hardware                 |
| CPU • RAM • Disk • Network Devices   |
+--------------------------------------+
```

⬅️ Previous: **[01-Introduction-to-Linux]( 01-Introduction-to-Linux.md)**

➡️ Next: **[ 03-Linux-Distributions](03-Linux-Distributions.md)**

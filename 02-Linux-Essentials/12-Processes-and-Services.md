# ⚙️ Linux Processes and Services

A **process** is a running instance of a program.

A **service** is a background process or application that provides a specific function to the system or other applications.

Understanding processes and services is essential for DevOps because you will regularly need to:

- Monitor applications
- Identify high CPU or memory usage
- Stop or restart processes
- Manage background applications
- Troubleshoot failed services
- Analyze logs
- Manage applications running on servers
- Automate service management

---

# 🧠 What is a Process?

When you execute a program, Linux creates a **process** to run it.

For example:

```bash
python3 app.py
```

Linux creates a process for:

```text
python3 app.py
```

Every process has a unique **Process ID (PID)**.

---

# 🆔 Process ID (PID)

A PID is a unique number assigned to a running process.

You can view processes using:

```bash
ps
```

Example:

```text
PID TTY          TIME CMD
1234 pts/0    00:00:00 bash
```

Here:

```text
1234 → PID
```

---

# 👑 PID 1

The first userspace process started by the Linux Kernel normally has:

```text
PID 1
```

On most modern Linux distributions using systemd:

```text
PID 1 → systemd
```

Check it:

```bash
ps -p 1 -f
```

or:

```bash
ps -p 1 -o pid,comm,args
```

PID 1 has an important role in:

- Starting system services
- Managing services
- Reaping orphaned processes
- Handling system initialization

---

# 🌳 Process Hierarchy

Linux processes form a hierarchy.

A process can create another process.

Example:

```text
systemd
   │
   ├── sshd
   │     └── bash
   │           └── python
   │
   ├── cron
   │
   └── nginx
         ├── nginx worker
         └── nginx worker
```

You can view process relationships using:

```bash
pstree
```

If `pstree` is not installed, it may need to be installed separately.

---

# 🔍 Viewing Processes with `ps`

`ps` provides a snapshot of currently running processes.

Basic:

```bash
ps
```

Show processes for all users:

```bash
ps aux
```

Another commonly used format:

```bash
ps -ef
```

---

# 📊 Understanding `ps aux`

Example:

```text
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  ...    ... ?        Ss   ...      ... /sbin/init
shubham   1234  0.2  1.0  ...    ... pts/0    S+   ...      ... bash
```

Important columns:

| Column | Meaning |
|---|---|
| `USER` | User running the process |
| `PID` | Process ID |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `VSZ` | Virtual memory size |
| `RSS` | Resident memory |
| `TTY` | Terminal |
| `STAT` | Process state |
| `START` | Start time |
| `TIME` | CPU time used |
| `COMMAND` | Command used to start the process |

---

# 📈 Monitoring Processes with `top`

`top` provides a real-time view of running processes and system resources.

Run:

```bash
top
```

It displays information such as:

- CPU usage
- Memory usage
- Load average
- Running processes
- Process IDs
- Process states

Useful keys inside `top` include:

```text
q → Quit
P → Sort by CPU
M → Sort by memory
k → Send a signal to a process
```

---

# 🖥️ `htop`

`htop` is an interactive process viewer.

Run:

```bash
htop
```

It provides a more user-friendly interface than `top`.

Depending on your Linux distribution, it may need to be installed:

```bash
sudo apt install htop
```

---

# 🔄 Process States

A process can be in different states.

Common states include:

| State | Meaning |
|---|---|
| `R` | Running or runnable |
| `S` | Interruptible sleep |
| `D` | Uninterruptible sleep |
| `T` | Stopped |
| `Z` | Zombie |
| `I` | Idle kernel thread |

You can see process states using:

```bash
ps aux
```

or:

```bash
ps -eo pid,stat,comm
```

---

# 🧟 Zombie Process

A **zombie process** is a process that has finished execution but still has an entry in the process table because its parent has not yet collected its exit status.

Example state:

```text
Z
```

You can search for zombie processes using:

```bash
ps aux | awk '$8 ~ /Z/ {print}'
```

A few zombies are not necessarily a problem, but a growing number may indicate an issue with the parent process.

---

# 👶 Parent and Child Processes

Processes can have:

- Parent Process ID (PPID)
- Child processes

View PPID:

```bash
ps -eo pid,ppid,comm
```

Example:

```text
PID   PPID  COMMAND
1000     1  sshd
1200  1000  bash
1300  1200  python3
```

Here:

```text
sshd
 ↓
bash
 ↓
python3
```

---

# 🌱 Orphan Processes

An orphan process is a process whose original parent has exited.

The process is adopted by another process, traditionally PID 1.

On modern Linux systems using systemd:

```text
Child Process
     ↓
Parent exits
     ↓
Re-parented
     ↓
PID 1 / system manager
```

---

# 🛑 Terminating Processes

## `kill`

The `kill` command sends a signal to a process.

Example:

```bash
kill 1234
```

By default, this sends:

```text
SIGTERM
```

---

# 📡 Common Signals

Some important signals include:

| Signal | Number | Purpose |
|---|---:|---|
| `SIGHUP` | 1 | Hangup |
| `SIGINT` | 2 | Interrupt |
| `SIGKILL` | 9 | Forcefully terminate |
| `SIGTERM` | 15 | Request termination |
| `SIGSTOP` | 19 | Stop process |

Terminate gracefully:

```bash
kill 1234
```

Explicitly send SIGTERM:

```bash
kill -15 1234
```

Forcefully terminate:

```bash
kill -9 1234
```

`SIGKILL` should be a last resort because the process cannot catch it or perform normal cleanup.

---

# 🎯 `pkill`

`pkill` can send signals to processes based on their name or other matching criteria.

Example:

```bash
pkill nginx
```

Use carefully because multiple processes may match.

---

# 🔎 `pgrep`

`pgrep` finds process IDs based on a process name or other criteria.

Example:

```bash
pgrep nginx
```

You can combine it with other commands:

```bash
pgrep -a nginx
```

---

# ⚡ Foreground and Background Processes

A command normally runs in the foreground.

Example:

```bash
ping google.com
```

The terminal remains attached to the process.

Press:

```text
Ctrl + C
```

to interrupt it.

---

# ⬇️ Running a Process in the Background

Add `&`:

```bash
ping google.com &
```

The command runs in the background.

Check background jobs:

```bash
jobs
```

---

# ⏸️ Suspend a Process

Press:

```text
Ctrl + Z
```

This suspends the foreground process.

Then:

```bash
jobs
```

to view it.

---

# ▶️ Resume a Process in the Background

Use:

```bash
bg
```

Example:

```bash
bg %1
```

---

# ⬆️ Bring a Process to the Foreground

Use:

```bash
fg
```

Example:

```bash
fg %1
```

---

# 🔢 Job IDs vs Process IDs

Do not confuse:

```text
Job ID
```

with:

```text
PID
```

Example:

```text
[1] 12345
```

Here:

```text
1     → Job ID
12345 → PID
```

Job IDs are managed by your shell, while PIDs are system-wide process identifiers.

---

# 🧰 `nohup`

`nohup` allows a command to continue running after the terminal session ends, subject to the process's own behavior and environment.

Example:

```bash
nohup python3 app.py &
```

By default, output may be redirected to:

```text
nohup.out
```

Check it:

```bash
tail -f nohup.out
```

This is useful for long-running commands when you do not need a full service manager.

For production applications, however, a proper service manager such as systemd is generally preferable.

---

# ⚙️ What is a Service?

A service is a background application or system component that provides functionality continuously or on demand.

Examples:

- SSH server
- Web server
- Database server
- Docker daemon
- Monitoring agents

Examples of common services:

```text
sshd
nginx
docker
cron
```

---

# 🧩 systemd

**systemd** is a system and service manager used by many modern Linux distributions.

It commonly runs as:

```text
PID 1
```

systemd manages different types of **units**, including:

- Services
- Sockets
- Timers
- Mounts
- Targets

---

# 🔧 `systemctl`

`systemctl` is used to interact with systemd.

Check system status:

```bash
systemctl status
```

Check a service:

```bash
systemctl status nginx
```

---

# ▶️ Start a Service

```bash
sudo systemctl start nginx
```

Check:

```bash
systemctl status nginx
```

---

# ⏹️ Stop a Service

```bash
sudo systemctl stop nginx
```

---

# 🔄 Restart a Service

```bash
sudo systemctl restart nginx
```

---

# 🔃 Reload a Service

Some services support configuration reloads without completely stopping the service.

```bash
sudo systemctl reload nginx
```

---

# 🔍 Check Whether a Service is Active

```bash
systemctl is-active nginx
```

---

# 🔌 Enable a Service at Boot

Enable:

```bash
sudo systemctl enable nginx
```

This configures the service to start according to its enabled boot configuration.

---

# 🚫 Disable a Service at Boot

```bash
sudo systemctl disable nginx
```

---

# ⚡ Enable and Start Together

Use:

```bash
sudo systemctl enable --now nginx
```

This enables the service and starts it immediately.

---

# 📋 List Services

List running service units:

```bash
systemctl list-units --type=service
```

List installed service unit files:

```bash
systemctl list-unit-files --type=service
```

---

# 📜 journalctl

`journalctl` is used to query logs stored in the **systemd journal**.

View logs:

```bash
journalctl
```

View logs from the current boot:

```bash
journalctl -b
```

Follow logs in real time:

```bash
journalctl -f
```

View logs for a specific service:

```bash
journalctl -u nginx
```

View recent service logs:

```bash
journalctl -u nginx -n 50
```

View service logs from the current boot:

```bash
journalctl -u nginx -b
```

---

# 🔗 Process vs Service

A process and a service are related but not exactly the same thing.

### Process

A process is a running instance of a program.

Example:

```text
python3 app.py
```

### Service

A service is a managed application or system component that provides functionality, often running in the background.

Example:

```text
nginx.service
```

A service can manage one or more processes.

---

# 📊 Process vs Service

| Process | Service |
|---|---|
| Running instance of a program | Managed background/system component |
| Has a PID | Usually represented by a systemd unit |
| Can be started by many mechanisms | Often managed by systemd |
| Can be temporary | Usually intended to provide ongoing functionality |
| Inspected using `ps`, `top`, etc. | Managed using `systemctl` |

---

# 🌍 Real-World DevOps Example

Imagine an NGINX web server is not responding.

First, check whether the service is running:

```bash
systemctl status nginx
```

Check whether an NGINX process exists:

```bash
pgrep -a nginx
```

Check listening ports:

```bash
ss -tuln
```

Check service logs:

```bash
journalctl -u nginx
```

Check system resources:

```bash
top
```

Test the web server locally:

```bash
curl http://localhost
```

This gives you several pieces of information:

```text
Service
  ↓
Process
  ↓
Port
  ↓
Logs
  ↓
Application response
```

---

# 🛠️ Hands-on Practice

Check your current processes:

```bash
ps
```

```bash
ps aux
```

Check PID 1:

```bash
ps -p 1 -f
```

Monitor processes:

```bash
top
```

Check memory:

```bash
free -h
```

Find a process:

```bash
pgrep -a bash
```

Check your background jobs:

```bash
jobs
```

Start a background process:

```bash
sleep 300 &
```

Check it:

```bash
jobs
```

Find its PID:

```bash
pgrep -a sleep
```

Terminate it:

```bash
kill <PID>
```

Verify:

```bash
pgrep -a sleep
```

---

# 🧪 Service Management Practice

On a system with an available service such as SSH, check:

```bash
systemctl status ssh
```

On some distributions the service may be named:

```bash
systemctl status sshd
```

Check whether it is active:

```bash
systemctl is-active ssh
```

View its logs:

```bash
journalctl -u ssh
```

Do not stop or restart critical services on a production machine unless you understand the impact.

---

# 🧪 Practice Challenge

Create a simple process-management workflow.

### Step 1

Start:

```bash
sleep 600 &
```

### Step 2

Find the process:

```bash
pgrep -a sleep
```

### Step 3

Inspect it:

```bash
ps -p <PID> -f
```

### Step 4

Check its state:

```bash
ps -p <PID> -o pid,ppid,stat,cmd
```

### Step 5

Terminate it gracefully:

```bash
kill <PID>
```

### Step 6

Verify:

```bash
pgrep -a sleep
```

Then practice the service-management workflow:

```text
systemctl status
        ↓
journalctl
        ↓
systemctl restart
        ↓
systemctl status
        ↓
curl / application test
```

---

# ⚠️ Important Safety Practices

Be careful when terminating processes.

Avoid blindly using:

```bash
kill -9
```

First try:

```bash
kill PID
```

which normally sends `SIGTERM`.

Use `SIGKILL` only when a process cannot be terminated gracefully.

Also be careful when restarting production services:

```bash
systemctl restart service
```

A restart can cause downtime or interrupt active connections.

Always identify the service and understand its role before changing its state.

---

# 💼 Interview Questions

- **What is a process in Linux?**  
  A process is a running instance of a program. Each process has a unique Process ID (PID).

- **What is a PID?**  
  PID stands for Process ID. It is the unique numeric identifier assigned to a running process.

- **What is PID 1?**  
  PID 1 is the first userspace process started by the Kernel. On most modern Linux systems using systemd, PID 1 is systemd.

- **What is the difference between `ps` and `top`?**  
  `ps` provides a snapshot of processes, while `top` provides a continuously updating interactive view.

- **What is `htop`?**  
  `htop` is an interactive process monitoring tool and an alternative to `top`.

- **What is a zombie process?**  
  A zombie is a process that has finished execution but still has an entry in the process table because its parent has not collected its exit status.

- **What is an orphan process?**  
  An orphan is a process whose original parent has exited. It is re-parented to another process, traditionally PID 1.

- **What does `kill` do?**  
  `kill` sends a signal to a process. By default, it normally sends `SIGTERM`.

- **What is the difference between `SIGTERM` and `SIGKILL`?**  
  `SIGTERM` requests that a process terminate gracefully and can be handled by the process. `SIGKILL` forcefully terminates the process and cannot be caught or ignored.

- **What is the difference between a process and a service?**  
  A process is a running instance of a program, while a service is a managed system or application component that often runs in the background and may manage one or more processes.

- **What is systemd?**  
  systemd is a system and service manager used by many modern Linux distributions and commonly runs as PID 1.

- **What is `systemctl` used for?**  
  `systemctl` is used to inspect and manage systemd units and services.

- **What is `journalctl` used for?**  
  `journalctl` is used to query logs stored in the systemd journal.

- **How do you start a service?**  
  Use:
  ```bash
  sudo systemctl start service-name
  ```

- **How do you stop a service?**  
  Use:
  ```bash
  sudo systemctl stop service-name
  ```

- **How do you restart a service?**  
  Use:
  ```bash
  sudo systemctl restart service-name
  ```

- **How do you enable a service to start during boot?**  
  Use:
  ```bash
  sudo systemctl enable service-name
  ```

- **How do you check whether a service is running?**  
  Use:
  ```bash
  systemctl status service-name
  ```
  or:
  ```bash
  systemctl is-active service-name
  ```

- **How do you view logs for a systemd service?**  
  Use:
  ```bash
  journalctl -u service-name
  ```

- **How would you troubleshoot a service that is not working?**  
  Check the service status with `systemctl`, inspect its logs using `journalctl`, check the related processes with `ps` or `pgrep`, inspect listening ports with `ss`, check system resources, and test the application itself.

- **Why is process and service management important for DevOps?**  
  DevOps engineers manage applications running on Linux servers, containers, and cloud infrastructure. Understanding processes and services is essential for deployment, monitoring, troubleshooting, and automation.

---

# 📚 Navigation

⬅️ Previous: **[11-Permissions.md](11-Permissions.md)**

➡️ Next: **[13-Storage.md](13-Storage.md)**

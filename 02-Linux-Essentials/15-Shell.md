# 🐚 Linux Shell

A **shell** is a command line interface that allows users to interact with the operating system.

Instead of using a graphical interface, you can use a shell to:

- Execute commands
- Manage files
- Start and stop processes
- Configure the system
- Run scripts
- Automate tasks
- Manage servers remotely

As a DevOps Engineer, strong shell knowledge is essential because most Linux servers are managed through the command line.

---

# 🧠 What is a Shell?

A shell is a program that accepts commands from the user and executes them.

The basic flow is:

```text
User
 ↓
Shell
 ↓
Operating System
 ↓
Kernel
 ↓
Hardware
```

For example:

```bash
ls
```

The shell receives the command and asks the operating system to execute it.

---

# 🐚 Common Linux Shells

Common shells include:

- Bash
- Zsh
- Fish
- Dash
- Ksh

Check your current shell:

```bash
echo $SHELL
```

Check the shell used by your current process:

```bash
ps -p $$ -o comm=
```

---

# 🟢 Bash

**Bash** stands for:

```text
Bourne Again Shell
```

Bash is one of the most widely used shells on Linux.

It provides:

- Command execution
- Variables
- Conditions
- Loops
- Functions
- Command history
- Aliases
- Job control
- Shell scripting

Bash is especially important for DevOps automation.

---

# 🔍 Check Available Shells

Linux maintains a list of commonly accepted login shells in:

```text
/etc/shells
```

View it:

```bash
cat /etc/shells
```

Example:

```text
/bin/sh
/bin/bash
/usr/bin/bash
/bin/dash
```

The exact list depends on the distribution.

---

# 📌 Environment Variables

Environment variables are named values available to processes.

Examples:

```text
HOME
PATH
USER
SHELL
PWD
```

View a variable:

```bash
echo $HOME
```

```bash
echo $USER
```

```bash
echo $SHELL
```

---

# 🔎 View Environment Variables

Use:

```bash
printenv
```

or:

```bash
env
```

You can also inspect shell variables and functions with:

```bash
set
```

`set` may produce a much larger amount of output because it includes shell variables and functions in addition to exported environment variables.

---

# 📦 Creating a Shell Variable

Create a variable:

```bash
name="Shubham"
```

Access it:

```bash
echo $name
```

Important:

```bash
name="Shubham"
```

Correct.

Do not add spaces around `=`:

```bash
name = "Shubham"
```

This is incorrect Bash syntax.

---

# 🌍 Environment Variables vs Shell Variables

A shell variable exists in the current shell.

Example:

```bash
name="Shubham"
```

An environment variable is exported so that child processes can inherit it.

Example:

```bash
export name="Shubham"
```

Check:

```bash
echo $name
```

---

# 👶 Child Processes

When a shell starts another process, that process can inherit exported environment variables.

Example:

```bash
export APP_ENV="development"
```

Run:

```bash
bash
```

Then:

```bash
echo $APP_ENV
```

The child shell can access the exported variable.

---

# 🛣️ PATH

`PATH` is one of the most important environment variables.

It tells the shell where to search for executable commands.

Check it:

```bash
echo $PATH
```

Example:

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Directories are separated by:

```text
:
```

---

# 🔍 How PATH Works

When you run:

```bash
python3
```

the shell searches directories listed in:

```text
$PATH
```

until it finds an executable named:

```text
python3
```

You can find the executable location using:

```bash
which python3
```

A more robust command lookup is:

```bash
command -v python3
```

---

# ➕ Adding a Directory to PATH

Temporarily add a directory:

```bash
export PATH="$PATH:$HOME/bin"
```

Check:

```bash
echo $PATH
```

This change applies to the current shell session.

For persistent configuration, the appropriate shell startup file must be configured.

---

# ⚠️ PATH Safety

Avoid blindly placing the current directory at the beginning of `PATH`:

```bash
export PATH=".:$PATH"
```

This can cause an unintended executable in the current directory to be run instead of a trusted system command.

Be especially careful when modifying `PATH` on production systems.

---

# 📌 Aliases

An alias creates a shortcut for a command.

Example:

```bash
alias ll='ls -lah'
```

Now:

```bash
ll
```

runs:

```bash
ls -lah
```

---

# 🔍 View Aliases

List aliases:

```bash
alias
```

Check one alias:

```bash
alias ll
```

---

# ❌ Removing an Alias

Use:

```bash
unalias ll
```

Remove all aliases:

```bash
unalias -a
```

Be careful with `unalias -a` because it removes all aliases from the current shell.

---

# 📋 Common Useful Aliases

Examples:

```bash
alias ll='ls -lah'
alias la='ls -A'
alias gs='git status'
```

Aliases are convenient, but avoid creating confusing aliases that hide important command behavior.

---

# 📁 Bash Configuration

Bash reads configuration files when starting different types of shell sessions.

Common files include:

```text
~/.bashrc
~/.bash_profile
~/.profile
```

The exact files loaded can depend on whether the shell is:

- Interactive
- Login
- Non-login

---

# 📝 `.bashrc`

A common file for interactive Bash configuration is:

```text
~/.bashrc
```

It can contain:

- Aliases
- Functions
- Environment configuration
- Shell options
- Prompt customization

View it:

```bash
cat ~/.bashrc
```

Edit it:

```bash
nano ~/.bashrc
```

or:

```bash
vim ~/.bashrc
```

---

# 🔄 Reload `.bashrc`

After changing `.bashrc`, you can reload it without opening a new shell:

```bash
source ~/.bashrc
```

Equivalent syntax:

```bash
. ~/.bashrc
```

---

# 📌 `.profile`

A common login-session configuration file is:

```text
~/.profile
```

It may be used to configure environment variables for login sessions.

View it:

```bash
cat ~/.profile
```

---

# 🧩 Shell Startup Files

A simplified view:

```text
Login Shell
    ↓
Profile configuration
    ↓
Interactive Shell
    ↓
.bashrc
```

The exact startup behavior depends on how Bash was launched.

This distinction becomes important when environment variables or commands appear to work in one terminal but not another.

---

# 🔤 Command History

Bash keeps a history of commands.

View history:

```bash
history
```

Run a previous command:

```bash
!100
```

where `100` is the history number.

Search command history interactively:

```text
Ctrl + R
```

---

# ⌨️ Useful Bash Shortcuts

| Shortcut | Purpose |
|---|---|
| `Ctrl + C` | Interrupt current process |
| `Ctrl + Z` | Suspend current process |
| `Ctrl + D` | End input / exit shell |
| `Ctrl + L` | Clear terminal screen |
| `Ctrl + R` | Search command history |
| `Ctrl + A` | Move to beginning of line |
| `Ctrl + E` | Move to end of line |
| `Ctrl + U` | Delete before cursor |
| `Ctrl + K` | Delete after cursor |
| `Tab` | Command/path completion |
| `↑` | Previous command |
| `↓` | Next command |

---

# 🔗 Command Chaining

The shell allows multiple commands to be combined.

Run commands sequentially:

```bash
command1; command2
```

Run the second command only if the first succeeds:

```bash
command1 && command2
```

Run the second command only if the first fails:

```bash
command1 || command2
```

Example:

```bash
mkdir project && cd project
```

If `mkdir` succeeds, the shell executes `cd project`.

---

# 📤 Output Redirection

Shells can redirect command output.

Write output to a file:

```bash
ls > files.txt
```

Append output:

```bash
ls >> files.txt
```

The difference:

```text
>  → Overwrite
>> → Append
```

---

# 📥 Input Redirection

A command can receive input from a file:

```bash
sort < names.txt
```

---

# 🚫 Standard Error

Linux commands have standard streams:

```text
stdin  → 0
stdout → 1
stderr → 2
```

Redirect standard error:

```bash
command 2> errors.txt
```

Redirect both stdout and stderr:

```bash
command > output.txt 2>&1
```

Modern Bash also supports:

```bash
command &> output.txt
```

---

# 🔗 Pipes

A pipe sends the output of one command to another command.

Example:

```bash
ps aux | grep nginx
```

Flow:

```text
ps aux
   ↓
Output
   ↓
grep nginx
```

Another example:

```bash
ls -l | less
```

---

# 🔢 Exit Status

Every command returns an exit status.

Usually:

```text
0 → Success
Non-zero → Failure
```

Check the previous command's exit status:

```bash
echo $?
```

Example:

```bash
ls
echo $?
```

If `ls` succeeds, you will normally see:

```text
0
```

---

# 🧠 Why Exit Codes Matter in DevOps

Exit codes are extremely important in:

- Bash scripts
- CI/CD pipelines
- Docker
- Kubernetes
- Automation
- Monitoring

For example:

```bash
command && echo "Success"
```

The second command runs only if the first command returns success.

---

# 📜 Shell Scripts

A shell script is a file containing shell commands.

Example:

```bash
#!/usr/bin/env bash

echo "Hello DevOps"
```

Save as:

```text
hello.sh
```

Run:

```bash
bash hello.sh
```

Or make it executable:

```bash
chmod +x hello.sh
```

Then:

```bash
./hello.sh
```

---

# 📝 Shebang

The first line of a script is often called the **shebang**.

Example:

```bash
#!/usr/bin/env bash
```

It tells the system which interpreter should execute the script when the file is run directly.

---

# 🔐 Shell and Permissions

A script must have execute permission to run directly:

```bash
./script.sh
```

Check:

```bash
ls -l script.sh
```

Add execute permission:

```bash
chmod +x script.sh
```

Then:

```bash
./script.sh
```

---

# 🌍 Real-World DevOps Example

Suppose you need to check whether a deployment directory exists.

You could run:

```bash
if [ -d /opt/myapp ]; then
    echo "Application directory exists"
else
    echo "Application directory does not exist"
fi
```

Shell scripting allows this type of logic to become part of:

- Deployment scripts
- Backup scripts
- Server maintenance
- CI/CD jobs
- Monitoring automation

Bash scripting will be covered in much greater depth in the dedicated **Bash Scripting** phase.

---

# 🤖 Shell in DevOps

Shell commands are everywhere in DevOps.

For example, a CI/CD pipeline may execute:

```bash
git clone ...
npm install
docker build .
docker push ...
kubectl apply ...
```

These commands can be executed by:

- GitHub Actions
- Jenkins
- GitLab CI
- Ansible
- Cloud-init
- Remote SSH sessions

Understanding the shell makes these tools much easier to work with.

---

# 🧪 Hands-on Practice

Check your shell:

```bash
echo $SHELL
```

Check your current process:

```bash
ps -p $$ -o comm=
```

Check environment variables:

```bash
printenv
```

Check `PATH`:

```bash
echo $PATH
```

Find a command:

```bash
command -v ls
```

Create a variable:

```bash
name="Shubham"
```

Print it:

```bash
echo $name
```

Export it:

```bash
export DEVOPS="Linux"
```

Check:

```bash
echo $DEVOPS
```

Create an alias:

```bash
alias ll='ls -lah'
```

Run:

```bash
ll
```

Remove it:

```bash
unalias ll
```

Check exit status:

```bash
true
echo $?
```

Then:

```bash
false
echo $?
```

---

# 🧪 Practice Challenge

Create a small shell environment practice.

### Step 1

Check your shell:

```bash
echo $SHELL
```

### Step 2

Check your `PATH`:

```bash
echo $PATH
```

### Step 3

Find the location of:

```bash
bash
ls
python3
git
```

using:

```bash
command -v
```

### Step 4

Create:

```bash
APP_NAME="DevOps"
```

Print it:

```bash
echo $APP_NAME
```

### Step 5

Export:

```bash
export ENVIRONMENT="development"
```

### Step 6

Create an alias:

```bash
alias ll='ls -lah'
```

### Step 7

Create:

```text
hello.sh
```

with:

```bash
#!/usr/bin/env bash

echo "Hello from Bash"
echo "Environment: $ENVIRONMENT"
```

Make it executable:

```bash
chmod +x hello.sh
```

Run:

```bash
./hello.sh
```

### Step 8

Check the exit status:

```bash
echo $?
```

---

# ⚠️ Shell Safety

Be careful when executing commands copied from the internet.

Understand commands before running them, especially commands involving:

```bash
sudo
rm
chmod
chown
curl
wget
```

Be particularly careful with commands that download and immediately execute scripts.

Avoid blindly executing:

```bash
curl ... | bash
```

unless you have verified and understand the source.

---

# 💼 Interview Questions

- **What is a shell?**  
  A shell is a command-line program that allows users to interact with the operating system by executing commands.

- **What is Bash?**  
  Bash stands for Bourne Again Shell and is one of the most widely used shells on Linux.

- **What is the difference between a shell and the Linux kernel?**  
  The shell provides a user interface for interacting with the operating system, while the kernel manages system resources and communicates with hardware.

- **How do you check the current shell?**  
  Use:
  ```bash
  echo $SHELL
  ```

- **What is an environment variable?**  
  An environment variable is a named value exported by a process environment and made available to child processes.

- **What is `PATH`?**  
  `PATH` is an environment variable containing directories where the shell searches for executable commands.

- **How do you check `PATH`?**  
  Use:
  ```bash
  echo $PATH
  ```

- **How do you find the location of an executable?**  
  Use:
  ```bash
  command -v command-name
  ```

- **What is an alias?**  
  An alias is a shortcut that maps a command name to another command or command string.

- **How do you create an alias?**  
  Example:
  ```bash
  alias ll='ls -lah'
  ```

- **How do you remove an alias?**  
  Use:
  ```bash
  unalias ll
  ```

- **What is `.bashrc`?**  
  `.bashrc` is commonly used for Bash interactive-shell configuration such as aliases, functions, and shell settings.

- **How do you reload `.bashrc`?**  
  Use:
  ```bash
  source ~/.bashrc
  ```

- **What is the difference between a shell variable and an environment variable?**  
  A shell variable exists in the current shell, while an exported environment variable is inherited by child processes.

- **What is command substitution?**  
  Command substitution allows the output of a command to be used as part of another command.
  Example:
  ```bash
  current_dir=$(pwd)
  ```

- **What is a pipe in Linux?**  
  A pipe sends the standard output of one command to the standard input of another command.
  Example:
  ```bash
  ps aux | grep nginx
  ```

- **What is output redirection?**  
  Output redirection sends command output to a file instead of the terminal.
  Example:
  ```bash
  ls > files.txt
  ```

- **What is the difference between `>` and `>>`?**  
  `>` overwrites the target file, while `>>` appends to it.

- **What is an exit status?**  
  An exit status is a numeric value returned by a command indicating whether it succeeded or failed. `0` normally represents success, while non-zero values indicate failure.

- **How do you check the exit status of the previous command?**  
  Use:
  ```bash
  echo $?
  ```

- **What is a shebang?**  
  A shebang is the first line of a script that specifies the interpreter used to execute the script, such as:
  ```bash
  #!/usr/bin/env bash
  ```

- **Why is shell knowledge important for DevOps?**  
  DevOps engineers frequently use Linux shells for server administration, automation, CI/CD pipelines, deployments, troubleshooting, and infrastructure management.

---

# 📚 Navigation

⬅️ Previous: **[14-Package-Management.md](14-Package-Management.md)**

➡️ Next: **[16-Hands-on-Labs.md](16-Hands-on-Labs.md)**

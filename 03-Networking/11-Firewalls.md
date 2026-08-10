# 🔥 Firewalls

## 🎯 What Are We Learning?

Imagine your house has:

```text
🏠 Home
   │
🚪 Main Gate
   │
   ├── 👨‍👩‍👧 Friends → ✅
   ├── 📦 Delivery → ✅
   └── 🕵️ Random Stranger → ❌
```

The gate doesn't care who you are emotionally. 😂

It follows rules:

```text
Who?
From where?
Going where?
Which door?
What type of traffic?
Allow or deny?
```

A network firewall does something similar.

> **Firewall = A security control that filters network traffic according to defined rules.**

---

# 🧠 Why Do We Need Firewalls?

Imagine a server connected directly to the Internet:

```text
🌍 Internet
     │
     │
     ↓
🖥️ Server
```

Without appropriate traffic controls, the server may receive unwanted connection attempts.

A firewall can create rules such as:

```text
Allow HTTPS :443
Allow SSH :22 from trusted network
Deny everything else
```

So:

```text
🌍 Internet
     │
     ↓
🔥 Firewall
     │
     ├── TCP 443 → ✅
     ├── SSH from trusted IP → ✅
     └── Unknown traffic → ❌
```

---

# 🏠 Real-Life Analogy

Think of a nightclub.

At the entrance:

```text
👮 Security
```

Security checks:

```text
Who are you?
Are you allowed inside?
Where are you from?
Do you meet the requirements?
```

A firewall performs a similar filtering function for network traffic.

---

# 🌐 What Does a Firewall Actually Do?

A firewall evaluates traffic against rules.

A simplified rule might say:

```text
Source:
10.0.0.0/24

Destination:
10.0.1.10

Protocol:
TCP

Port:
443

Action:
ALLOW
```

Meaning:

```text
10.0.0.0/24
      ↓
TCP :443
      ↓
10.0.1.10
      ↓
✅ ALLOW
```

Another rule might be:

```text
Source:
0.0.0.0/0

Destination:
10.0.1.10

Protocol:
TCP

Port:
22

Action:
DENY
```

Meaning:

```text
🌍 Internet
      ↓
SSH :22
      ↓
❌ DENY
```

---

# 🧩 Firewall Components

A firewall rule commonly considers:

```text
Source
Destination
Protocol
Port
Direction
Action
```

Let's understand each.

---

# 📍 Source

The source is where the traffic comes from.

Example:

```text
192.168.1.10
```

or:

```text
10.0.0.0/24
```

or:

```text
0.0.0.0/0
```

---

# 🎯 Destination

The destination is where the traffic is going.

Example:

```text
10.0.2.20
```

or:

```text
10.0.2.0/24
```

---

# 🚚 Protocol

The firewall can filter based on protocol.

Examples:

```text
TCP
UDP
ICMP
```

---

# 🚪 Port

For TCP/UDP traffic, firewalls can filter ports.

Examples:

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
```

---

# ↔️ Direction

Traffic can be:

```text
Inbound
Outbound
```

### Inbound

Traffic coming toward your system.

```text
🌍 Internet
     ↓
🔥 Firewall
     ↓
🖥️ Server
```

### Outbound

Traffic leaving your system.

```text
🖥️ Server
     ↓
🔥 Firewall
     ↓
🌍 Internet
```

---

# 🟢 Allow vs 🔴 Deny

A firewall rule needs an action.

Common actions:

```text
ALLOW
DENY
REJECT
```

The exact behavior depends on the firewall technology.

---

# 🆚 DROP vs REJECT

These are worth understanding.

### DROP

The firewall silently discards the packet.

Conceptually:

```text
Client
  ↓
🔥 Firewall
  X
(no response)
```

### REJECT

The firewall actively responds that the traffic is not allowed, using an appropriate rejection mechanism.

Conceptually:

```text
Client
  ↓
🔥 Firewall
  ↓
❌ Rejected
```

Think:

```text
DROP
→ "Ignore it."

REJECT
→ "No, you're not allowed."
```

---

# 🧠 Stateful vs Stateless Firewalls

This is an important concept.

---

# 🧠 Stateful Firewall

A stateful firewall keeps track of connection state.

Example:

```text
Client
   ↓
TCP Connection
   ↓
Server
```

The firewall remembers that the connection was established.

If the server sends valid return traffic:

```text
Server
   ↓
Firewall
   ↓
Client
```

the firewall can recognize it as part of an established connection.

Think:

> 🧠 "I remember this conversation."

---

# 📜 Stateless Firewall

A stateless firewall evaluates packets primarily against rules without maintaining the same connection-state awareness.

Think:

> 📋 "I will inspect this packet according to my rules."

---

# 🆚 Stateful vs Stateless

| Feature | Stateful | Stateless |
|---|---|---|
| Tracks connection state | ✅ | ❌ |
| Understands established connections | ✅ | Limited |
| Rule evaluation | State + packet | Packet/rule based |
| Common use | Host/network firewalls | ACL-style filtering |

---

# 🏠 Real-Life Analogy

### Stateful

Security guard remembers:

> "You entered 10 minutes ago, so I know you're part of the group."

### Stateless

Security guard checks you from scratch every time:

> "Show your pass again."

😂

---

# 🔥 Firewall vs Router vs NAT

These are different concepts.

```text
📡 Router
→ Decides where traffic should go

🔄 NAT
→ Translates addresses/ports

🔥 Firewall
→ Controls whether traffic is allowed
```

A single device can perform multiple functions.

For example:

```text
Home Router
│
├── Routing
├── NAT/PAT
└── Firewall
```

But conceptually, the functions are different.

---

# 🔥 Firewall vs NAT

We already learned NAT.

Remember:

```text
NAT
→ Address translation

Firewall
→ Traffic filtering
```

NAT does not replace a firewall.

---

# 🌐 Firewall Types

You may encounter different types of firewalls.

Common categories include:

```text
Host-based firewall
Network firewall
Stateful firewall
Stateless firewall
Web Application Firewall
Cloud firewall/security controls
```

Let's understand the important ones.

---

# 💻 Host-Based Firewall

A host-based firewall runs directly on a machine.

Example:

```text
🖥️ Linux Server
     │
     └── 🔥 Firewall
```

It controls traffic entering or leaving that host.

Examples on Linux include:

```text
nftables
iptables
UFW
firewalld
```

---

# 🌐 Network Firewall

A network firewall sits between networks.

Example:

```text
🌍 Internet
     ↓
🔥 Firewall
     ↓
🏢 Internal Network
```

It can protect many systems at once.

---

# 🌐 Web Application Firewall

A WAF stands for:

```text
Web Application Firewall
```

It is designed to protect web applications by inspecting HTTP/HTTPS traffic and applying application-layer rules.

Example:

```text
🌍 Internet
     ↓
🔥 WAF
     ↓
⚖️ Load Balancer
     ↓
🖥️ Web Application
```

A WAF can help protect against certain web attacks such as:

```text
SQL Injection
Cross-Site Scripting
Malicious HTTP requests
```

The exact protections depend on the WAF configuration and rules.

---

# 🧠 Firewall Layers

A firewall may inspect different kinds of information.

For example:

```text
Layer 3
↓
IP addresses

Layer 4
↓
TCP/UDP
Ports

Layer 7
↓
Application traffic
```

A traditional network firewall may focus heavily on:

```text
IP
Protocol
Port
Connection state
```

A WAF focuses on:

```text
HTTP/HTTPS
URLs
Headers
Parameters
Application requests
```

---

# ☁️ AWS Security Controls

AWS provides multiple networking security mechanisms.

Important ones for your DevOps journey include:

```text
Security Groups
Network ACLs
AWS WAF
Network Firewall
```

We'll focus on the first three concepts first.

---

# ☁️ AWS Security Groups

A Security Group acts as a virtual firewall for supported AWS resources such as EC2 instances.

It controls traffic based on rules such as:

```text
Protocol
Port
Source/Destination
```

Example:

```text
Security Group

Inbound:
TCP 22
Source: My IP
        ↓
       ALLOW

Inbound:
TCP 443
Source: 0.0.0.0/0
        ↓
       ALLOW
```

Conceptually:

```text
🌍 Internet
      │
      ↓
🛡️ Security Group
      │
      ↓
🖥️ EC2
```

---

# 🔐 Security Group Example

Imagine an application server:

```text
EC2
10.0.1.10
```

You want:

```text
HTTPS → Everyone
SSH → Only your IP
```

Rules:

```text
Inbound

TCP 443
Source: 0.0.0.0/0
Action: ALLOW

TCP 22
Source: YOUR_PUBLIC_IP/32
Action: ALLOW
```

This is much safer than:

```text
TCP 22
Source: 0.0.0.0/0
```

unless you have a specific reason and compensating controls.

---

# 🚨 Why `0.0.0.0/0` Matters

In IPv4:

```text
0.0.0.0/0
```

means:

```text
Any IPv4 address
```

So:

```text
SSH :22
Source 0.0.0.0/0
```

means:

> Any IPv4 source can attempt to reach SSH.

That can expose your server to Internet-wide scanning and attack attempts.

Better:

```text
SSH :22
Source: Your trusted IP
```

or use a more secure access architecture such as:

```text
VPN
Bastion
SSM
Zero Trust access
```

depending on the environment.

---

# ☁️ Network ACL

AWS Network ACLs, or NACLs, operate at the subnet level.

Conceptually:

```text
VPC
│
├── Subnet A
│      ↓
│   Network ACL
│      ↓
│   EC2
│
└── Subnet B
       ↓
    Network ACL
       ↓
      EC2
```

They can control inbound and outbound traffic for subnet interfaces.

---

# 🆚 Security Group vs NACL

| Feature | Security Group | Network ACL |
|---|---|---|
| Scope | Resource/network interface level | Subnet level |
| Stateful | ✅ | ❌ |
| Rules | Allow rules | Allow + Deny |
| Return traffic | Automatically handled by state | Must be considered explicitly |
| Common use | Instance/resource access control | Subnet-level filtering |

A useful mental model:

```text
Security Group
→ "Can this resource communicate?"

NACL
→ "Can traffic enter/leave this subnet?"
```

---

# 🧠 Important AWS Rule

Don't confuse:

```text
Security Group
```

with:

```text
NACL
```

Security Groups are **stateful**.

NACLs are **stateless**.

That distinction appears frequently in interviews.

---

# 🐧 Linux Firewalls

Linux provides several firewall technologies and management tools.

You will encounter:

```text
Netfilter
nftables
iptables
UFW
firewalld
```

---

# 🧠 Netfilter

Netfilter is the Linux kernel's networking framework that provides packet filtering, NAT, and related networking functionality.

Tools such as:

```text
iptables
nftables
```

interact with this framework.

Think:

```text
Linux Kernel
     │
     ↓
Netfilter
     │
     ├── nftables
     └── iptables
```

---

# 🧩 nftables

Modern Linux systems commonly use:

```text
nftables
```

for packet filtering and related networking rules.

Inspect rules with:

```bash
sudo nft list ruleset
```

Don't modify rules on your main environment unless you understand the consequences.

---

# 🧩 iptables

You may still see:

```bash
iptables
```

in many tutorials, existing servers, and older infrastructure.

Example inspection:

```bash
sudo iptables -L -n -v
```

For NAT:

```bash
sudo iptables -t nat -L -n -v
```

Remember:

> `iptables` is still important to understand because you will encounter it in real systems, even as nftables becomes the modern Linux direction.

---

# 🧩 UFW

UFW stands for:

```text
Uncomplicated Firewall
```

It provides a simpler interface for managing firewall rules on Ubuntu and Debian-based systems.

Check status:

```bash
sudo ufw status
```

Example rule:

```bash
sudo ufw allow 22/tcp
```

Example:

```bash
sudo ufw allow 443/tcp
```

---

# 🧩 firewalld

`firewalld` is a firewall management solution commonly encountered on distributions such as:

```text
RHEL
Fedora
Rocky Linux
AlmaLinux
```

Check status:

```bash
sudo firewall-cmd --state
```

List configuration:

```bash
sudo firewall-cmd --list-all
```

---

# 🆚 UFW vs firewalld

| Tool | Commonly Seen With |
|---|---|
| UFW | Ubuntu/Debian |
| firewalld | RHEL/Fedora family |
| nftables | Modern Linux |
| iptables | Legacy/existing environments |

The underlying implementation can vary by distribution and version.

---

# 🧪 Linux Firewall Investigation

On your WSL Ubuntu environment, start with:

```bash
sudo ufw status
```

You may get:

```text
Status: inactive
```

That's okay.

WSL networking is different from a typical production Linux server.

Then inspect:

```bash
sudo nft list ruleset
```

If the environment has no relevant rules, don't worry.

The goal is understanding the concepts.

---

# 🔎 Check Listening Ports

A firewall rule is useless if there is no application listening.

Run:

```bash
ss -lntup
```

Example:

```text
LISTEN
0.0.0.0:22
```

means a service is listening on TCP port 22.

Your troubleshooting should be:

```text
🔥 Firewall
       ↓
🚪 Port
       ↓
🖥️ Application
```

not just:

> "Port 443 is allowed, so the website must work."

---

# 🚨 Important Troubleshooting Rule

Suppose:

```text
TCP 443
```

is allowed.

But:

```text
Nothing is listening on 443.
```

The connection still won't work.

So:

```text
Firewall allows traffic
       ≠
Application is healthy
```

---

# 🧪 Real DevOps Troubleshooting

Suppose users say:

> 🚨 "Our website is unreachable."

You investigate systematically.

---

## Step 1 — DNS

```bash
dig example.com
```

Does the domain resolve?

---

## Step 2 — Route

```bash
ip route get SERVER_IP
```

Is traffic taking the expected path?

---

## Step 3 — Port

```bash
ss -lntup
```

Is the application listening?

---

## Step 4 — Firewall

Check:

```text
Host firewall
Cloud firewall
Network firewall
Security Group
NACL
WAF
```

---

## Step 5 — Application

Test:

```bash
curl -v https://example.com
```

---

# 🧠 Troubleshooting Flow

```text
🌐 DNS
   ↓
📍 IP
   ↓
🛣️ Route
   ↓
🔥 Firewall
   ↓
🚪 Port
   ↓
🔐 TLS
   ↓
🌐 HTTP
   ↓
🖥️ Application
```

This is the kind of flow you should build into your brain.

---

# 🧩 Firewall Rule Evaluation

Suppose you have:

```text
Rule 1:
Allow TCP 443

Rule 2:
Deny TCP 22
```

Then:

```text
HTTPS → ✅
SSH   → ❌
```

But the exact rule-processing behavior depends on the firewall implementation.

Some firewalls use:

```text
First match
```

Others can use different rule evaluation models.

So always understand the specific firewall's rule-processing logic.

---

# 🧠 Default Deny

A strong security principle is:

> **Allow only what is required.**

Conceptually:

```text
Default:
❌ DENY

Explicit:
443 → ✅
22 from trusted IP → ✅
```

This is often called:

```text
Default Deny
```

or:

```text
Least Privilege
```

---

# 🔐 Least Privilege

Don't give more access than necessary.

Bad:

```text
Allow:
Everything
Everyone
Every port
```

Better:

```text
Allow:
HTTPS
From:
Required sources
To:
Required destination
```

This principle appears everywhere in DevOps and cybersecurity.

---

# 🌍 Example: Web Application

Suppose:

```text
🌍 Internet
      ↓
⚖️ Load Balancer
      ↓
🖥️ Application Server
      ↓
🗄️ Database
```

You don't want:

```text
Internet → Database :5432
```

Instead:

```text
Internet
   ↓
HTTPS :443
   ↓
Load Balancer
   ↓
Application
   ↓
Database :5432
```

Firewall rules can enforce this segmentation.

---

# 🗄️ Database Security Example

Suppose PostgreSQL uses:

```text
5432
```

Bad:

```text
Internet
   ↓
TCP 5432
   ↓
Database
```

Better:

```text
Application Subnet
      ↓
TCP 5432
      ↓
Database
```

So the database firewall/security rules should allow only the required application sources.

---

# 🏗️ Three-Tier Architecture

A common architecture:

```text
                 🌍 Internet
                      │
                      ↓
               🔥 Public Firewall
                      │
                      ↓
                ⚖️ Load Balancer
                      │
                      ↓
              🖥️ Application Tier
                      │
                      ↓
                 🗄️ Database
```

Security policy:

```text
Internet
   ↓
HTTPS :443
   ↓
Load Balancer

Load Balancer
   ↓
Application Port
   ↓
Application

Application
   ↓
Database Port
   ↓
Database
```

Not:

```text
Internet
   ↓
Everything
   ↓
Everything
```

---

# ☁️ AWS Example

Imagine:

```text
🌍 Internet
      ↓
⚖️ ALB
      ↓
🖥️ EC2
      ↓
🗄️ RDS
```

Security Groups could be:

```text
ALB Security Group
────────────────────
Allow TCP 443
Source: Internet


EC2 Security Group
────────────────────
Allow application port
Source: ALB Security Group


RDS Security Group
────────────────────
Allow TCP 5432
Source: EC2 Security Group
```

Notice the security relationship:

```text
Internet
   ↓
ALB
   ↓
EC2
   ↓
RDS
```

Each layer only exposes what it needs.

---

# 🚨 Common Mistakes

## ❌ Opening SSH to the entire Internet

```text
TCP 22
0.0.0.0/0
```

Avoid this unless there's a deliberate reason and strong compensating controls.

---

## ❌ Opening database ports publicly

For example:

```text
TCP 3306
0.0.0.0/0
```

or:

```text
TCP 5432
0.0.0.0/0
```

This is generally a serious security mistake.

---

## ❌ Assuming firewall = security

Firewalls are one security layer.

You also need:

```text
Authentication
Authorization
Encryption
Patch Management
Monitoring
Logging
Secrets Management
Application Security
```

---

## ❌ Forgetting outbound traffic

Security isn't only about inbound traffic.

Applications also make outbound connections:

```text
Application
   ↓
DNS
   ↓
API
   ↓
Package Repository
   ↓
Cloud Service
```

Outbound rules matter too.

---

# 🧪 Hands-on Mission

Run these commands on your Linux environment.

### Mission 1

```bash
sudo ufw status
```

Record:

```text
UFW Status:
```

---

### Mission 2

```bash
sudo nft list ruleset
```

Look for:

```text
tables
chains
rules
```

---

### Mission 3

```bash
ss -lntup
```

Record a few listening ports:

```text
Port:
Protocol:
Process:
```

---

### Mission 4

Check your routes:

```bash
ip route
```

Think:

```text
Traffic
 ↓
Route
 ↓
Firewall
 ↓
Port
 ↓
Application
```

---

# 🎮 Firewall Challenge

You have:

```text
Web Server:
10.0.1.10
```

Required:

```text
HTTPS → Everyone
SSH → Admin IP only
Database → No Internet access
```

Design the rules:

| Source | Destination | Protocol | Port | Action |
|---|---|---|---:|---|
| Internet | Web Server | TCP | 443 | Allow |
| Admin IP | Web Server | TCP | 22 | Allow |
| Internet | Web Server | TCP | 22 | Deny |
| Internet | Database | TCP | 5432 | Deny |

Now think:

```text
🌍 Internet
    │
    ├── HTTPS → 🖥️ Web → ✅
    │
    ├── SSH → 🖥️ Web → ❌
    │
    └── DB → 🗄️ Database → ❌
```

---

# 🎮 Scenario Challenge

Your application:

```text
10.0.1.10:8080
```

Your firewall allows:

```text
TCP 443
```

But users still cannot connect.

What could be wrong?

Possible reasons:

```text
DNS points to wrong IP
Routing problem
Load balancer isn't forwarding correctly
Port 443 isn't listening
Application is listening on 8080 instead
Security Group/NACL blocks traffic
Firewall blocks traffic
TLS configuration problem
Application is unhealthy
```

Notice how firewall is only **one** part of the investigation.

---

# 🧠 Firewall Cheat Sheet

```text
🔥 Firewall
→ Filters traffic

📍 Source
→ Where traffic comes from

🎯 Destination
→ Where traffic goes

🚚 Protocol
→ TCP / UDP / ICMP

🚪 Port
→ Application entry point

🟢 ALLOW
→ Permit

🔴 DENY
→ Block

🗑️ DROP
→ Silently discard

🚫 REJECT
→ Explicitly reject

🧠 Stateful
→ Tracks connection state

📋 Stateless
→ Doesn't maintain connection state in the same way

💻 Host Firewall
→ Protects one machine

🌐 Network Firewall
→ Protects network boundaries

🔥 WAF
→ Filters web/application traffic
```

---

# 💼 Interview Corner

### Q: What is a firewall?

> A firewall is a security control that filters network traffic according to defined rules.

---

### Q: What can firewall rules be based on?

Common criteria include:

```text
Source
Destination
Protocol
Port
Direction
Connection state
```

---

### Q: What is a stateful firewall?

> A stateful firewall tracks connection state and can use that information when evaluating traffic.

---

### Q: What is a stateless firewall?

> A stateless firewall evaluates traffic primarily against configured rules without maintaining connection state in the same way a stateful firewall does.

---

### Q: What is the difference between DROP and REJECT?

> DROP silently discards traffic, while REJECT actively indicates that the traffic was not accepted.

---

### Q: Is NAT a firewall?

```text
No ❌
```

NAT:

```text
Address translation
```

Firewall:

```text
Traffic filtering
```

---

### Q: What is a WAF?

> A Web Application Firewall filters and protects HTTP/HTTPS application traffic using web-focused rules.

---

### Q: What is a Security Group in AWS?

> An AWS Security Group is a stateful virtual firewall associated with supported AWS resources such as network interfaces/EC2 instances to control inbound and outbound traffic.

---

### Q: What is a Network ACL?

> An AWS Network ACL is a stateless subnet-level network filtering control that supports allow and deny rules.

---

### Q: Security Group vs NACL?

```text
Security Group
→ Stateful
→ Resource/interface level
→ Allow rules

NACL
→ Stateless
→ Subnet level
→ Allow + Deny rules
```

---

### Q: What is least privilege?

> Grant only the minimum network access required for a system or service to perform its function.

---

### Q: Why shouldn't a database be publicly exposed?

> Exposing a database directly to the Internet unnecessarily increases its attack surface. It is generally better to restrict database access to the application components that require it.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain firewalls
- [ ] Explain why firewalls are needed
- [ ] Explain firewall rules
- [ ] Explain source
- [ ] Explain destination
- [ ] Explain protocols
- [ ] Explain ports
- [ ] Explain inbound traffic
- [ ] Explain outbound traffic
- [ ] Explain ALLOW
- [ ] Explain DENY
- [ ] Explain DROP
- [ ] Explain REJECT
- [ ] Explain stateful firewalls
- [ ] Explain stateless firewalls
- [ ] Explain host-based firewalls
- [ ] Explain network firewalls
- [ ] Explain WAF
- [ ] Explain firewall vs NAT
- [ ] Explain Linux firewall concepts
- [ ] Recognize nftables
- [ ] Recognize iptables
- [ ] Recognize UFW
- [ ] Recognize firewalld
- [ ] Explain AWS Security Groups
- [ ] Explain AWS NACLs
- [ ] Compare Security Groups and NACLs
- [ ] Understand least privilege
- [ ] Troubleshoot basic firewall problems
- [ ] Explain firewall use in Docker
- [ ] Explain firewall/network security in Kubernetes
- [ ] Explain firewall security in AWS

---

# 🎯 Mini Project

## 🏗️ Design a Secure 3-Tier Application

Design:

```text
                    🌍 Internet
                         │
                         ↓
                  ⚖️ Load Balancer
                         │
                         ↓
                  🖥️ Application
                         │
                         ↓
                    🗄️ Database
```

Requirements:

```text
1. Internet users can access HTTPS.

2. Only the load balancer can reach the application.

3. Only the application can reach the database.

4. SSH should only be available from an administrator's trusted IP/network.

5. The database should not be publicly reachable.

6. Unnecessary traffic should be denied.
```

Create:

### Network Diagram

```text
Internet
   │
   ↓
Load Balancer
   │
   ↓
Application
   │
   ↓
Database
```

### Security Rules

| Component | Source | Protocol | Port | Action |
|---|---|---|---:|---|
| Load Balancer | Internet | TCP | 443 | Allow |
| Application | Load Balancer | TCP | 8080 | Allow |
| Database | Application | TCP | 5432 | Allow |
| Application | Admin Network | TCP | 22 | Allow |
| Database | Internet | TCP | 5432 | Deny |

Then answer:

```text
1. Why is the database not publicly accessible?

2. Why is HTTPS open to the Internet?

3. Why should SSH be restricted?

4. What is the difference between a Security Group and NACL?

5. Where would a WAF fit?

6. Where would NAT fit if the private application server needs outbound Internet access?
```

---

# 🔥 DevOps Connection

Now your networking foundation is becoming seriously useful.

You've learned:

```text
IP
 ↓
Subnet
 ↓
Routing
 ↓
NAT
 ↓
Protocols
 ↓
DNS
 ↓
Firewall
```

Put that into a real cloud architecture:

```text
                         🌍 Internet
                              │
                              ↓
                          DNS
                              │
                              ↓
                         🔥 WAF
                              │
                              ↓
                       ⚖️ Load Balancer
                              │
                              ↓
                     🔒 Application Subnet
                              │
                              ↓
                       🗄️ Database Subnet
```

And for outbound traffic:

```text
Private Application
        ↓
   Route Table
        ↓
   NAT Gateway
        ↓
Internet Gateway
        ↓
      Internet
```

This is the foundation you'll use later for:

```text
☁️ AWS
🐳 Docker
☸️ Kubernetes
🔐 DevSecOps
🚀 CI/CD
🏗️ Infrastructure as Code
```

The goal isn't to memorize firewall commands.

The goal is to look at a production architecture and immediately ask:

```text
Who can talk to whom?
On which protocol?
On which port?
From which network?
Through which route?
And why is that access required?
```

That's the security mindset you want as a DevOps / Platform Engineer. 🔥

---

# 📚 Navigation

⬅️ Previous: **[10-DNS.md](10-DNS.md)**

➡️ Next: **[12-Load-Balancing.md](12-Load-Balancing.md)**

🏠 Networking Phase: **[README.md](README.md)**

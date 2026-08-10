# 🔐 Network Security

## 🎯 What Are We Learning?

So far, we've learned how networks communicate:

```text
IP Addressing
      ↓
Subnetting
      ↓
Routing
      ↓
NAT
      ↓
DNS
      ↓
Firewalls
      ↓
Load Balancing
      ↓
VPC
      ↓
VPC Peering
      ↓
VPN
```

Now comes the big question:

> **How do we stop the wrong traffic from reaching the right systems?** 😄

Imagine your house:

```text
🏠 Your House
   │
   ├── 🚪 Main Door
   ├── 🔒 Door Lock
   ├── 🚨 Alarm
   ├── 📹 CCTV
   └── 🧱 Boundary Wall
```

Your network needs similar layers of protection.

```text
🌍 Internet
     ↓
🔥 Firewall
     ↓
⚖️ Load Balancer
     ↓
🖥️ Application
     ↓
🗄️ Database
```

This is the basic idea of:

> **Network Security**

---

# 🧠 What Is Network Security?

Network security is the practice of protecting:

```text
Networks
Systems
Applications
Data
Traffic
```

from:

```text
Unauthorized Access
Attacks
Data Theft
Malicious Traffic
Network Abuse
```

A simple mental model:

```text
👤 User
   ↓
🌐 Network
   ↓
🛡️ Security Controls
   ↓
🖥️ Application
```

---

# 🏠 Real-Life Example

Imagine a large office building:

```text
🏢 Office
```

Anyone shouldn't be able to walk into:

```text
🔐 Server Room
```

So the company might have:

```text
🚪 Main Gate
   ↓
🪪 ID Check
   ↓
🛡️ Security Guard
   ↓
🔐 Server Room
```

In networking:

```text
🌍 Internet
   ↓
🔥 Firewall
   ↓
🛡️ Authentication
   ↓
🖥️ Server
```

Different controls solve different problems.

---

# 🎯 Goals of Network Security

A classic way to think about security is the:

> **CIA Triad**

```text
🔒 Confidentiality
🧩 Integrity
⚡ Availability
```

---

# 🔒 Confidentiality

Confidentiality means:

> Only authorized people or systems should be able to access information.

Example:

```text
🗄️ Customer Database
```

A random Internet user:

```text
🌍 Hacker
   ↓
❌ No Access
```

Authorized application:

```text
🖥️ Application
   ↓
✅ Allowed
```

---

# 🧩 Integrity

Integrity means:

> Data should not be modified by unauthorized parties.

Example:

```text
Original:
₹10,000
```

An attacker shouldn't be able to change it to:

```text
₹1
```

without authorization.

---

# ⚡ Availability

Availability means:

> Systems and services should remain accessible when authorized users need them.

Example:

```text
🌍 Users
   ↓
🖥️ Website
```

If attackers overwhelm the website:

```text
🔥 Traffic
   ↓
💥 Server
   ↓
❌ Website Down
```

availability is affected.

---

# 🧠 CIA Triad Example

Imagine an online banking application.

### Confidentiality

```text
Only you can see your account details.
```

### Integrity

```text
Your balance can't be changed by an attacker.
```

### Availability

```text
The banking service should remain accessible.
```

---

# 🛡️ Defense in Depth

One of the most important security concepts is:

> **Defense in Depth**

Don't rely on one security control.

Instead:

```text
🌍 Internet
     ↓
🔥 WAF
     ↓
🛡️ Firewall
     ↓
⚖️ Load Balancer
     ↓
🛡️ Security Group
     ↓
🖥️ Application
     ↓
🛡️ Security Group
     ↓
🗄️ Database
```

If one layer fails, other layers still provide protection.

---

# 🏰 Real-Life Analogy

Think about a castle:

```text
🏰 Castle
│
├── 🧱 Outer Wall
├── 🚪 Gate
├── 🛡️ Guards
├── 🚪 Inner Door
└── 🔐 Treasury
```

An attacker has to get through multiple layers.

Network security follows the same philosophy.

---

# 🔥 Firewall

A firewall controls network traffic based on defined rules.

Basic idea:

```text
Traffic
   ↓
🔥 Firewall
   ↓
Allow / Deny
```

Example:

```text
Allow TCP 443
Deny TCP 23
```

Meaning:

```text
HTTPS → ✅
Telnet → ❌
```

---

# 🧠 Firewall Rule

A firewall rule commonly considers things such as:

```text
Source
Destination
Protocol
Port
Action
```

Example:

```text
Source:
10.0.1.0/24

Destination:
10.0.2.10

Protocol:
TCP

Port:
443

Action:
ALLOW
```

---

# 🚪 Ports

Remember:

```text
IP Address
→ Which machine?

Port
→ Which service?
```

Example:

```text
10.0.1.10:443
```

means:

```text
10.0.1.10
     ↓
TCP Port 443
     ↓
HTTPS Service
```

---

# 📋 Common Ports

| Port | Protocol / Service | Typical Use |
|---:|---|---|
| 22 | SSH | Remote administration |
| 53 | DNS | Name resolution |
| 80 | HTTP | Web traffic |
| 443 | HTTPS | Secure web traffic |
| 25 | SMTP | Email transfer |
| 110 | POP3 | Email retrieval |
| 143 | IMAP | Email retrieval |
| 3306 | MySQL | Database |
| 5432 | PostgreSQL | Database |
| 6379 | Redis | Cache/database |

> Don't open ports simply because they exist. Only expose the services that are actually required.

---

# 🚨 Principle of Least Privilege

One of the most important security principles:

> **Give only the access that is actually required.**

Bad:

```text
🌍 Internet
   ↓
🖥️ Server
   ↓
Allow:
ALL PORTS
ALL PROTOCOLS
ALL SOURCES
```

😬 That's basically saying:

> "Welcome everyone, please make yourself comfortable."

---

Better:

```text
Internet
   ↓
TCP 443
   ↓
Load Balancer
```

Application:

```text
Load Balancer
   ↓
TCP 443
   ↓
Application
```

Database:

```text
Application
   ↓
TCP 5432
   ↓
Database
```

Only the required traffic is allowed.

---

# 🛡️ Security Groups

In AWS, Security Groups act as stateful virtual firewalls for supported resources.

Example:

```text
Internet
   ↓
ALB
   ↓
Security Group
   ↓
Application
```

Rules can control:

```text
Protocol
Port
Source
```

---

# 🔄 Stateful Firewall

A stateful firewall remembers connection state.

Example:

```text
Client
  ↓
Request
  ↓
Server
  ↓
Response
  ↓
Client
```

If the initial connection is permitted, the response traffic can be allowed as part of the established connection according to the firewall's stateful behavior.

---

# 🧱 Network ACL

A Network ACL operates at the subnet level.

Architecture:

```text
VPC
 │
 └── Subnet
       │
       ↓
     NACL
       │
       ↓
    Resources
```

A NACL is:

```text
Stateless
```

and supports:

```text
ALLOW
DENY
```

rules.

---

# 🆚 Security Group vs NACL

| Feature | Security Group | NACL |
|---|---|---|
| Scope | Resource/network-interface level | Subnet level |
| Stateful | ✅ | ❌ |
| Rules | Allow | Allow + Deny |
| Applied to | Supported resources | Subnet |
| Typical role | Resource-level control | Subnet-level boundary |

---

# 🧠 Easy Memory Trick

```text
Security Group
→ "Protect this resource."

NACL
→ "Control traffic entering/leaving this subnet."
```

---

# 🌐 Public vs Private Resources

One of the best security practices is:

> Don't make something public unless it needs to be public.

Bad architecture:

```text
🌍 Internet
 ├── 🖥️ App
 ├── 🗄️ Database
 ├── 🖥️ Internal API
 └── 🔧 Admin Server
```

Better:

```text
🌍 Internet
     ↓
⚖️ Load Balancer
     ↓
🔒 Private Application
     ↓
🔒 Private Database
```

---

# 🏗️ Three-Tier Security Architecture

A common architecture:

```text
                    🌍 Internet
                         │
                         ↓
                      ⚖️ ALB
                         │
                         ↓
              🔒 Application Tier
                /             \
              App 1          App 2
                \             /
                 \           /
                  ↓         ↓
              🔒 Database Tier
                    │
                    ↓
                 🗄️ DB
```

Security should be layered between these tiers.

---

# 🔐 Example Security Groups

## ALB Security Group

Allow:

```text
HTTPS 443
Source:
Internet
```

---

## Application Security Group

Allow:

```text
HTTPS / required application port
Source:
ALB Security Group
```

---

## Database Security Group

Allow:

```text
TCP 5432
Source:
Application Security Group
```

Result:

```text
🌍 Internet
    ↓
TCP 443
    ↓
ALB
    ↓
Application
    ↓
TCP 5432
    ↓
Database
```

The database is not directly exposed to the Internet.

---

# 🔐 Security Group Referencing

In AWS, Security Groups can often be referenced as sources for traffic rules between supported resources.

Instead of:

```text
Database SG

Allow:
10.0.2.0/24
```

you can conceptually define:

```text
Database SG

Allow:
Application SG
```

This is often cleaner because access follows the application architecture rather than relying on manually maintained IP ranges.

---

# 🌐 Network Segmentation

Network segmentation means dividing a network into different security zones.

Example:

```text
VPC
│
├── 🌐 Public Zone
│
├── 🔒 Application Zone
│
└── 🗄️ Database Zone
```

Each zone can have different:

```text
Routes
Firewall Rules
Security Groups
Access Policies
```

---

# 🧱 Why Segment Networks?

Suppose an attacker compromises:

```text
Application Server
```

Without segmentation:

```text
Attacker
   ↓
Application
   ↓
Everything 😱
```

With segmentation:

```text
Attacker
   ↓
Application
   ↓
❌ Database access blocked
❌ Admin network blocked
❌ Internal services blocked
```

The attacker's movement can be limited.

---

# 🚨 Lateral Movement

Lateral movement means:

> An attacker moves from one compromised system to other systems inside the environment.

Example:

```text
🌍 Attacker
     ↓
Compromised Server
     ↓
Internal Server
     ↓
Database
```

Network segmentation and least privilege can reduce this risk.

---

# 🔥 WAF

A:

> **Web Application Firewall (WAF)**

protects web applications by inspecting HTTP/HTTPS requests and applying rules against unwanted web traffic.

Architecture:

```text
🌍 Internet
     ↓
🔥 WAF
     ↓
⚖️ Load Balancer
     ↓
🖥️ Application
```

---

# 🧠 Firewall vs WAF

### Network Firewall

Generally focuses on network traffic such as:

```text
IP
Protocol
Port
Network flow
```

### WAF

Focuses on:

```text
HTTP
HTTPS
URLs
Headers
Requests
Web attack patterns
```

---

# 🆚 Firewall vs WAF

| Feature | Firewall | WAF |
|---|---|---|
| Main focus | Network traffic | Web application traffic |
| IP filtering | ✅ | Can be part of rules |
| Port filtering | ✅ | Not its main purpose |
| HTTP-aware | Not necessarily | ✅ |
| Web attack protection | Limited/general | Specialized |
| Typical position | Network boundary | In front of web application |

---

# 🧪 Example Web Request

User sends:

```http
GET /login HTTP/1.1
Host: example.com
```

A WAF can inspect the HTTP request and apply web security rules.

Flow:

```text
Client
  ↓
🌐 HTTP Request
  ↓
🔥 WAF
  ↓
⚖️ Load Balancer
  ↓
🖥️ Application
```

---

# 🛡️ DDoS Protection

A:

> **Distributed Denial-of-Service (DDoS)**

attack attempts to overwhelm a service with large amounts of traffic or requests.

Conceptually:

```text
😈 😈 😈 😈 😈
 \  |  |  |  /
       ↓
   🖥️ Website
       ↓
      💥
```

The goal is to affect:

```text
Availability
```

---

# 🧠 DDoS vs Normal Traffic

Normal:

```text
👤 👤 👤
  ↓ ↓ ↓
Server
```

Attack:

```text
😈 😈 😈 😈 😈 😈 😈 😈
        ↓↓↓↓↓↓↓
       Server
          💥
```

Cloud providers offer DDoS protection services and infrastructure designed to help absorb and mitigate certain attacks.

---

# 🔐 Encryption in Transit

Data traveling across networks should be protected when confidentiality is required.

Example:

```text
Client
  ↓
🔐 HTTPS
  ↓
Server
```

Common technologies include:

```text
TLS
HTTPS
VPN/IPsec
SSH
```

---

# 🗄️ Encryption at Rest

Data stored on disks or storage systems can also be encrypted.

Example:

```text
🗄️ Database
   ↓
🔐 Encrypted Storage
```

Remember:

```text
In Transit
→ Data moving

At Rest
→ Data stored
```

---

# 🆚 In Transit vs At Rest

| Type | Meaning | Example |
|---|---|---|
| In Transit | Data moving | HTTPS |
| At Rest | Data stored | Encrypted disk |
| In Use | Data actively processed | Application memory |

---

# 🔑 Authentication vs Authorization

These are often confused.

## Authentication

> "Who are you?"

Example:

```text
Username
+
Password
```

or:

```text
MFA
Certificate
Token
```

---

## Authorization

> "What are you allowed to do?"

Example:

```text
User:
Read logs

Admin:
Read + Delete logs
```

---

# 🧠 Easy Memory Trick

```text
Authentication
→ Who are you?

Authorization
→ What can you do?
```

---

# 🔐 MFA

> **Multi-Factor Authentication**

requires more than one authentication factor.

Example:

```text
Password
    +
OTP
```

or:

```text
Password
    +
Security Key
```

This reduces the risk of account compromise when a password is stolen.

---

# 🪪 IAM

Cloud environments use:

> **Identity and Access Management**

to control:

```text
Users
Roles
Permissions
Services
Resources
```

Network security and IAM are different but complementary.

Example:

```text
IAM
→ Can this user call the AWS API?

Network Security
→ Can this machine communicate with that service?
```

---

# 🧠 Network Security vs IAM

```text
IAM
"Are you allowed to perform this action?"

Network Security
"Can this traffic reach this resource?"
```

You often need both.

---

# 🚨 Zero Trust

A modern security principle is:

> **Never automatically trust a user or system just because it is inside the network.**

Instead:

```text
Verify
   ↓
Authenticate
   ↓
Authorize
   ↓
Allow minimum access
   ↓
Monitor
```

---

# 🏢 Old Mental Model

Traditional thinking:

```text
🌍 Internet
    ↓
🔥 Firewall
    ↓
🏢 Trusted Internal Network
```

Everything inside was often treated as relatively trusted.

---

# 🔐 Zero Trust Mental Model

```text
User
 ↓
Authenticate
 ↓
Verify
 ↓
Authorize
 ↓
Minimum Access
 ↓
Resource
```

Even internal traffic should be evaluated according to policy.

---

# 🧠 Zero Trust Principles

Think:

```text
🔎 Verify explicitly
🔒 Use least privilege
📊 Assume breach
👀 Continuously monitor
```

---

# 📊 Logging and Monitoring

Security isn't only about blocking traffic.

You also need to know:

> "What happened?"

Useful information includes:

```text
Source IP
Destination IP
Port
Protocol
Timestamp
Action
User
Resource
```

Example:

```text
10:32:11
Source: 203.0.113.10
Destination: 10.0.2.10
Port: 443
Action: ALLOW
```

---

# 🔍 Network Security Monitoring

Useful tools/concepts include:

```text
Flow Logs
Firewall Logs
WAF Logs
Application Logs
DNS Logs
System Logs
```

These help with:

```text
Troubleshooting
Incident Response
Security Investigations
Compliance
Auditing
```

---

# 🚨 Intrusion Detection

An:

> **IDS — Intrusion Detection System**

detects suspicious activity.

Conceptually:

```text
Traffic
  ↓
🔎 IDS
  ↓
🚨 Alert
```

---

# 🛡️ Intrusion Prevention

An:

> **IPS — Intrusion Prevention System**

can detect and potentially block malicious traffic.

Conceptually:

```text
Traffic
  ↓
🛡️ IPS
  ↓
Allow / Block
```

---

# 🆚 IDS vs IPS

| Feature | IDS | IPS |
|---|---|---|
| Detects threats | ✅ | ✅ |
| Alerts | ✅ | ✅ |
| Blocks traffic | Usually ❌ | ✅ |
| Position | Monitoring | Inline/prevention |

---

# 🏗️ Complete Network Security Architecture

Let's combine everything:

```text
                         🌍 Internet
                              │
                              ↓
                           🔥 WAF
                              │
                              ↓
                        ⚖️ Load Balancer
                              │
                     🛡️ Security Group
                              │
                ┌─────────────┴─────────────┐
                ↓                           ↓
          🔒 Application 1            🔒 Application 2
                │                           │
                └─────────────┬─────────────┘
                              ↓
                       🛡️ Security Group
                              │
                              ↓
                         🗄️ Database
```

Additional security:

```text
        🔍 Monitoring
             │
             ↓
      Logs / Flow Logs
```

And:

```text
IAM
 ↓
Identity + Permissions
```

---

# ☁️ AWS Security Architecture

A simplified AWS design:

```text
                         🌍 Internet
                              │
                              ↓
                           Route 53
                              │
                              ↓
                            🔥 WAF
                              │
                              ↓
                     ⚖️ Application LB
                              │
                              ↓
                    🔒 Private Subnets
                    /               \
                   ↓                 ↓
                 EC2               EC2
                   │                 │
                   └────────┬────────┘
                            ↓
                     🔒 Database SG
                            │
                            ↓
                         🗄️ RDS
```

Security layers:

```text
WAF
 ↓
Load Balancer
 ↓
Security Groups
 ↓
NACL
 ↓
Private Subnets
 ↓
IAM
 ↓
Encryption
 ↓
Logging + Monitoring
```

---

# 🧪 Hands-on Lab

## Mission 1 — Inspect Your Linux Firewall

Depending on your Linux distribution, you may encounter:

```bash
ufw status
```

or:

```bash
sudo nft list ruleset
```

or:

```bash
sudo iptables -L
```

Don't blindly change firewall rules on a machine you depend on.

First:

```text
Observe
Understand
Then Modify
```

---

# 🧪 Mission 2 — Check Listening Services

Run:

```bash
ss -lntup
```

Find:

```text
Port
Protocol
Address
Process
```

Create a table:

| Port | Protocol | Service | Should it be exposed? |
|---:|---|---|---|
| | | | |
| | | | |
| | | | |

---

# 🧪 Mission 3 — Test a Port

Use:

```bash
nc -vz example.com 443
```

Compare with a port that should not normally be open.

Remember:

> A failed connection doesn't automatically mean a firewall is the problem.

Other possibilities include:

```text
No service listening
Routing
DNS
Application configuration
Network policy
```

---

# 🧪 Mission 4 — Inspect Routes

Run:

```bash
ip route
```

Answer:

```text
What is the default gateway?

What interface is being used?

What network is directly connected?
```

---

# 🧪 Mission 5 — DNS Investigation

Run:

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

Identify:

```text
DNS Server
Resolved IP
Record Type
```

---

# 🎮 Security Challenge

You have:

```text
🌍 Internet
      ↓
    ALB
      ↓
Application
      ↓
Database
```

Requirements:

```text
Internet → ALB
ALB → Application
Application → Database
```

But:

```text
Internet → Database ❌
Internet → Application ❌
Database → Internet ❌
```

Design the Security Groups.

### Suggested design:

```text
ALB SG
Allow:
TCP 443
Source:
Internet
```

```text
Application SG
Allow:
Application port
Source:
ALB SG
```

```text
Database SG
Allow:
TCP 5432
Source:
Application SG
```

This creates:

```text
🌍 Internet
     ↓
   ALB
     ↓
 Application
     ↓
 Database
```

instead of:

```text
🌍 Internet
 ├──→ ALB
 ├──→ Application ❌
 └──→ Database ❌
```

---

# 🎮 Challenge 2 — Find the Security Problem

Architecture:

```text
🌍 Internet
     ↓
🖥️ EC2
```

Security Group:

```text
TCP 22
Source:
0.0.0.0/0
```

Question:

> What is the concern?

### Answer:

SSH is exposed to the entire IPv4 Internet.

A better approach is to restrict administrative access to trusted sources or use a more secure administrative access architecture.

---

# 🎮 Challenge 3

Database Security Group:

```text
TCP 5432
Source:
0.0.0.0/0
```

What's wrong?

### Answer:

The database port is exposed to all IPv4 sources.

A better design:

```text
Application SG
      ↓
TCP 5432
      ↓
Database
```

---

# 🎮 Challenge 4

You have:

```text
Security Group → ALLOW
```

but traffic still fails.

What else should you check?

```text
Route Table
NACL
Firewall
DNS
Application
Listening Port
Return Path
```

---

# 🧠 Security Troubleshooting Mindset

Never say:

> "It must be the firewall."

Instead think:

```text
1. DNS
   ↓
2. Routing
   ↓
3. Network Reachability
   ↓
4. Security Group
   ↓
5. NACL
   ↓
6. Firewall
   ↓
7. Port
   ↓
8. Application
```

This mindset will save you a LOT of debugging time in DevOps.

---

# 💼 Interview Corner

### Q: What is network security?

> Network security is the practice of protecting networks, systems, services, and traffic from unauthorized access, attacks, and misuse.

---

### Q: What is the CIA Triad?

```text
Confidentiality
Integrity
Availability
```

---

### Q: What is defense in depth?

> Using multiple independent security layers instead of relying on a single security control.

---

### Q: What is least privilege?

> Giving users, systems, and services only the minimum access required to perform their tasks.

---

### Q: What is a Security Group?

> An AWS Security Group is a stateful virtual firewall associated with supported resources/network interfaces that controls allowed traffic.

---

### Q: What is a NACL?

> A Network ACL is a stateless subnet-level network access control mechanism.

---

### Q: Security Group vs NACL?

```text
Security Group
→ Stateful
→ Resource/network-interface level
→ Allow rules

NACL
→ Stateless
→ Subnet level
→ Allow + Deny rules
```

---

### Q: What is a WAF?

> A Web Application Firewall filters and inspects HTTP/HTTPS traffic to help protect web applications from unwanted or malicious requests.

---

### Q: Firewall vs WAF?

```text
Firewall
→ Network traffic

WAF
→ Web application traffic
```

---

### Q: What is encryption in transit?

> Protecting data while it is moving across a network, commonly using technologies such as TLS or IPsec.

---

### Q: What is encryption at rest?

> Protecting stored data using encryption.

---

### Q: Authentication vs Authorization?

```text
Authentication
→ Who are you?

Authorization
→ What can you do?
```

---

### Q: What is Zero Trust?

> A security approach that does not automatically trust users or systems based only on network location and instead continuously evaluates identity, access, and context.

---

### Q: What is IDS?

> An Intrusion Detection System detects suspicious activity and generates alerts.

---

### Q: What is IPS?

> An Intrusion Prevention System can detect and block suspicious or malicious traffic.

---

### Q: Why should databases normally be private?

> Databases generally don't need direct Internet access. Keeping them private reduces the attack surface and allows access to be restricted to trusted application components.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain Network Security
- [ ] Explain CIA Triad
- [ ] Explain Confidentiality
- [ ] Explain Integrity
- [ ] Explain Availability
- [ ] Explain Defense in Depth
- [ ] Explain Least Privilege
- [ ] Explain Firewalls
- [ ] Explain Firewall Rules
- [ ] Explain Ports
- [ ] Explain Security Groups
- [ ] Explain Stateful Filtering
- [ ] Explain NACLs
- [ ] Compare Security Groups and NACLs
- [ ] Explain WAF
- [ ] Compare Firewall and WAF
- [ ] Explain DDoS
- [ ] Explain Encryption in Transit
- [ ] Explain Encryption at Rest
- [ ] Explain Authentication
- [ ] Explain Authorization
- [ ] Explain MFA
- [ ] Explain IAM
- [ ] Explain Zero Trust
- [ ] Explain Network Segmentation
- [ ] Explain Lateral Movement
- [ ] Explain IDS
- [ ] Explain IPS
- [ ] Explain Security Monitoring
- [ ] Troubleshoot blocked network traffic
- [ ] Design secure public/private architecture
- [ ] Apply least privilege to network access

---

# 🎯 Mini Project

## 🔐 Secure Three-Tier AWS Application

Design a secure production-style architecture:

```text
                         🌍 Internet
                              │
                              ↓
                           Route 53
                              │
                              ↓
                            🔥 WAF
                              │
                              ↓
                         ⚖️ ALB
                              │
                    ┌─────────┴─────────┐
                    ↓                   ↓
                 AZ-1                 AZ-2
                    │                   │
             🔒 Private App       🔒 Private App
                    │                   │
                    └─────────┬─────────┘
                              ↓
                       🔒 Database Tier
                         /          \
                        ↓            ↓
                     🗄️ DB-A      🗄️ DB-B
```

---

# 🛡️ Security Requirements

### Internet

Allow:

```text
HTTPS 443
```

to:

```text
ALB
```

---

### ALB

Allow:

```text
HTTPS 443
```

from:

```text
Internet
```

---

### Application

Allow:

```text
Required application port
```

from:

```text
ALB Security Group
```

---

### Database

Allow:

```text
TCP 5432
```

from:

```text
Application Security Group
```

---

### Administration

Do NOT automatically allow:

```text
SSH 22
Source: 0.0.0.0/0
```

Instead use a restricted administration strategy.

---

# 🧠 Final Architecture

```text
                     🌍 Internet
                          │
                          ↓
                       🔥 WAF
                          │
                          ↓
                    ⚖️ Load Balancer
                          │
              ┌───────────┴───────────┐
              ↓                       ↓
          🔒 App AZ-1             🔒 App AZ-2
              │                       │
              └───────────┬───────────┘
                          ↓
                    🔒 Database
                          │
                          ↓
                       🗄️ DB
```

Security layers:

```text
WAF
 ↓
Load Balancer
 ↓
Security Groups
 ↓
Private Subnets
 ↓
NACL
 ↓
IAM
 ↓
Encryption
 ↓
Logging
 ↓
Monitoring
```

---

# 🔥 DevOps Connection

This is where networking becomes **DevSecOps**.

You've now learned:

```text
Networking
     ↓
Cloud Networking
     ↓
Network Security
```

And the real production mindset becomes:

```text
🌍 Who is connecting?
        ↓
🔐 Are they authenticated?
        ↓
🛡️ Are they authorized?
        ↓
🛣️ Can the traffic reach the resource?
        ↓
🔥 Is the traffic allowed?
        ↓
🔒 Is the data protected?
        ↓
📊 Are we monitoring it?
```

A secure DevOps architecture isn't:

```text
"Put a firewall in front of it." 😂
```

It's:

```text
Identity
+
Network Segmentation
+
Least Privilege
+
Encryption
+
Firewalls
+
Secure Architecture
+
Monitoring
+
Continuous Verification
```

That's the foundation you'll build on when you move into:

```text
☁️ AWS Security
🏗️ Terraform Security
🐳 Docker Security
☸️ Kubernetes Network Policies
🔐 DevSecOps
🚀 Secure CI/CD
📊 Security Monitoring
```

---

# 📚 Navigation

⬅️ Previous: **[15-VPN.md](15-VPN.md)**

➡️ Next: **[17-Network-Troubleshooting.md](17-Network-Troubleshooting.md)**

🏠 Networking Phase: **[README.md](README.md)**

# 🌐 Networking Fundamentals


Networking is the foundation of communication between computers, servers, applications, cloud resources, containers, and users.

As a DevOps Engineer, you need to understand how systems communicate, how data travels across networks, how services are exposed, and how to troubleshoot connectivity problems.

---

# 🌍 What is Networking?

A computer network is a group of connected devices that communicate and exchange data.

Common network devices include:

```text
Computers
Servers
Routers
Switches
Firewalls
Load Balancers
Cloud Resources
Containers
```

Basic communication:

```text
Client
   ↓
Network
   ↓
Router
   ↓
Server
   ↓
Application
```

Example:

When you open:

```text
https://example.com
```

your system communicates with a remote server using multiple networking components and protocols.

---

# 🧩 Basic Networking Components

## 💻 Client

A client initiates communication with another system.

Examples:

```text
Web Browser
Mobile Application
curl
API Client
```

---

## 🖥️ Server

A server provides services or resources to clients.

Examples:

```text
Web Server
Application Server
Database Server
DNS Server
Mail Server
```

---

## 🔀 Switch

A switch connects devices within a local network.

Example:

```text
PC ─────┐
        │
PC ─────┼──── Switch
        │
Server ─┘
```

---

## 🌐 Router

A router connects different networks and forwards packets between them.

Example:

```text
Local Network
      ↓
    Router
      ↓
   Internet
```

---

## 🛡️ Firewall

A firewall controls network traffic according to configured rules.

Rules can be based on:

```text
Source
Destination
Protocol
Port
Direction
```

---

# 📦 How Network Communication Works

When an application sends data, the data moves through different networking layers.

A simplified representation:

```text
Application Data
       ↓
    Segment
       ↓
     Packet
       ↓
     Frame
       ↓
      Bits
```

Each layer adds information required for communication.

---

# 🏗️ OSI Model

The **OSI Model** stands for:

```text
Open Systems Interconnection
```

It is a conceptual model used to understand network communication.

The OSI model has seven layers:

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

---

# 📊 OSI Layers

| Layer | Name | Main Responsibility | Examples |
|---:|---|---|---|
| 7 | Application | Network services for applications | HTTP, DNS, SSH |
| 6 | Presentation | Data representation | Encoding, Encryption, Compression |
| 5 | Session | Session management | Session establishment |
| 4 | Transport | End-to-end communication | TCP, UDP, Ports |
| 3 | Network | Logical addressing and routing | IP, Routers |
| 2 | Data Link | Local network communication | Ethernet, MAC |
| 1 | Physical | Transmission of bits | Cable, Fiber, Radio |

The OSI model will be covered in detail in:

```text
02-OSI-Model.md
```

---

# 🌐 TCP/IP Model

The TCP/IP model is the practical networking model used by modern Internet-based communication.

A common four-layer representation is:

```text
4. Application
3. Transport
2. Internet
1. Network Access
```

Mapping to OSI:

| OSI | TCP/IP |
|---|---|
| Application | Application |
| Presentation | Application |
| Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link | Network Access |
| Physical | Network Access |

The TCP/IP model will be covered in detail in:

```text
03-TCP-IP-Model.md
```

---

# 🌍 IP Addressing

An IP address identifies a network interface using the Internet Protocol.

Examples:

```text
192.168.1.10
10.0.0.5
172.16.1.20
```

IP addressing allows systems to communicate across networks.

There are two major versions:

```text
IPv4
IPv6
```

---

# 4️⃣ IPv4

IPv4 uses:

```text
32-bit addresses
```

Example:

```text
192.168.1.10
```

An IPv4 address contains four octets:

```text
192 . 168 . 1 . 10
```

Each octet can have a value from:

```text
0 - 255
```

---

# 6️⃣ IPv6

IPv6 uses:

```text
128-bit addresses
```

Example:

```text
2001:db8::1
```

IPv6 provides a vastly larger address space than IPv4.

IPv4 and IPv6 will be covered separately in:

```text
04-IPv4.md
05-IPv6.md
```

---

# 🧮 Subnetting

Subnetting divides a larger IP network into smaller logical networks.

For example:

```text
10.0.0.0/24
```

can be divided into smaller networks.

Subnetting is useful for:

- Network organization
- IP address management
- Routing
- Security
- Traffic isolation
- Cloud network design

Detailed subnetting will be covered in:

```text
06-Subnetting.md
```

---

# 🛣️ Routing

Routing is the process of determining where network packets should be forwarded.

Basic flow:

```text
Source
  ↓
Router
  ↓
Routing Table
  ↓
Next Hop
  ↓
Destination
```

Linux routing table:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

Routing will be covered in:

```text
07-Routing.md
```

---

# 🔄 NAT

NAT stands for:

```text
Network Address Translation
```

NAT translates addresses between different network address spaces.

A common example:

```text
Private Network
      ↓
NAT
      ↓
Public IP
      ↓
Internet
```

NAT is commonly used when private systems need to communicate with public networks.

Detailed NAT concepts will be covered in:

```text
08-NAT.md
```

---

# 🔌 Network Protocols

Protocols define how systems communicate.

Important protocols for DevOps include:

```text
HTTP
HTTPS
SSH
DNS
DHCP
FTP
SMTP
```

---

## 🌐 HTTP

HTTP stands for:

```text
Hypertext Transfer Protocol
```

It is widely used for communication between clients and web servers.

Basic flow:

```text
Client
  ↓
HTTP Request
  ↓
Web Server
  ↓
HTTP Response
```

Common HTTP methods:

```text
GET
POST
PUT
PATCH
DELETE
```

---

## 🔒 HTTPS

HTTPS is HTTP secured using TLS.

It provides security properties including:

- Encryption
- Authentication
- Integrity protection

HTTPS is widely used for secure web communication.

---

## 🔐 SSH

SSH stands for:

```text
Secure Shell
```

It provides secure remote access to systems.

Example:

```bash
ssh user@server
```

SSH is heavily used by DevOps Engineers for:

- Remote server administration
- Troubleshooting
- Automation
- Secure command execution

---

## 🌎 DNS

DNS stands for:

```text
Domain Name System
```

DNS translates domain names into IP addresses and can provide other DNS information.

Example:

```text
example.com
     ↓
    DNS
     ↓
192.0.2.10
```

---

## 📡 DHCP

DHCP stands for:

```text
Dynamic Host Configuration Protocol
```

It can automatically provide clients with:

```text
IP Address
Subnet Information
Default Gateway
DNS Server
```

---

## 📁 FTP

FTP stands for:

```text
File Transfer Protocol
```

It is designed for transferring files.

For secure file transfers, technologies such as SFTP are commonly used.

---

## 📧 SMTP

SMTP stands for:

```text
Simple Mail Transfer Protocol
```

It is used for sending and relaying email.

---

# 🔢 Ports

A port identifies a transport-layer service endpoint.

Examples:

| Protocol | Common Port |
|---|---:|
| SSH | 22 |
| DNS | 53 |
| HTTP | 80 |
| HTTPS | 443 |
| SMTP | 25 |

A single IP address can have multiple services using different ports.

Example:

```text
192.168.1.10:22
192.168.1.10:80
192.168.1.10:443
```

---

# 🐧 Linux Networking

Linux provides many tools for inspecting and troubleshooting networking.

Important commands:

```text
ip
ping
traceroute
curl
wget
dig
nslookup
ss
netstat
```

---

# 📡 `ping`

Tests basic IP connectivity using ICMP echo messages.

```bash
ping 8.8.8.8
```

Test a hostname:

```bash
ping example.com
```

Stop:

```text
Ctrl + C
```

---

# 🛣️ `traceroute`

Shows the network hops between your system and a destination.

```bash
traceroute example.com
```

It can help identify where traffic stops progressing.

---

# 🌐 `curl`

`curl` is commonly used to communicate with network services.

Example:

```bash
curl https://example.com
```

Show HTTP headers:

```bash
curl -I https://example.com
```

Verbose mode:

```bash
curl -v https://example.com
```

Common DevOps uses:

```text
API Testing
HTTP Testing
Health Checks
Troubleshooting
Automation
```

---

# 📥 `wget`

`wget` is commonly used to download files.

Example:

```bash
wget https://example.com/file.zip
```

---

# 🔍 `dig`

`dig` is a DNS troubleshooting tool.

Example:

```bash
dig example.com
```

Query an A record:

```bash
dig example.com A
```

Query nameservers:

```bash
dig example.com NS
```

---

# 🔎 `nslookup`

`nslookup` can query DNS information.

```bash
nslookup example.com
```

It is useful for basic DNS troubleshooting.

---

# 🔌 `ss`

`ss` displays socket and network connection information.

Show listening TCP sockets:

```bash
ss -ltn
```

Show listening TCP and UDP sockets:

```bash
ss -lntup
```

Show established TCP connections:

```bash
ss -tn
```

---

# 📋 `netstat`

`netstat` is an older networking utility.

Example:

```bash
netstat -tulnp
```

On many modern Linux systems, `netstat` is not installed by default.

The modern replacement is generally:

```bash
ss
```

---

# 🧭 `ip`

The `ip` command is a modern Linux networking utility.

Show IP addresses:

```bash
ip addr
```

Show interfaces:

```bash
ip link
```

Show routing table:

```bash
ip route
```

---

# ☁️ Cloud Networking

Networking becomes extremely important in cloud environments.

Important concepts include:

```text
VPC
Subnets
Route Tables
Internet Gateway
NAT Gateway
Security Groups
Load Balancers
Reverse Proxy
CDN
VPN
```

These concepts will be covered in:

```text
11-Cloud-Networking-Concepts.md
```

---

# 🧪 Basic Network Troubleshooting

When troubleshooting networking problems, follow a structured approach.

```text
Network Interface
       ↓
IP Configuration
       ↓
Routing
       ↓
DNS
       ↓
Port
       ↓
Protocol
       ↓
Application
```

---

# 🔧 Step 1 — Check Interface

```bash
ip addr
```

Check whether the interface exists and has an IP address.

---

# 🔧 Step 2 — Check Routing

```bash
ip route
```

Look for an appropriate:

```text
default route
```

---

# 🔧 Step 3 — Test Local Networking

```bash
ping 127.0.0.1
```

---

# 🔧 Step 4 — Test Gateway

Find the gateway:

```bash
ip route
```

Then:

```bash
ping <gateway-ip>
```

---

# 🔧 Step 5 — Test External Connectivity

```bash
ping 8.8.8.8
```

If external IP connectivity works but hostname resolution fails, DNS may be the problem.

---

# 🔧 Step 6 — Test DNS

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

---

# 🔧 Step 7 — Test HTTP

```bash
curl -I https://example.com
```

---

# 🔧 Step 8 — Check Listening Ports

```bash
ss -lntup
```

Check whether the expected service is listening.

---

# 🧠 Example Troubleshooting Flow

Suppose:

```bash
curl https://example.com
```

fails.

Investigate:

```bash
ip addr
```

↓

```bash
ip route
```

↓

```bash
ping 8.8.8.8
```

↓

```bash
dig example.com
```

↓

```bash
ss -lntup
```

↓

```bash
curl -v https://example.com
```

This helps narrow down whether the problem is related to:

```text
Interface
IP
Route
DNS
Port
TLS
HTTP
Application
```

---

# 🧪 Hands-on Practice

## Lab 1 — Identify Your Network

Run:

```bash
ip addr
```

```bash
ip route
```

```bash
hostname
```

Document:

```text
Hostname:
Interface:
IPv4 Address:
IPv6 Address:
Default Gateway:
```

---

## Lab 2 — Test Connectivity

Test:

```bash
ping 127.0.0.1
```

Then:

```bash
ping 8.8.8.8
```

Then:

```bash
ping example.com
```

Compare the results.

---

## Lab 3 — DNS

Run:

```bash
dig example.com
```

Then:

```bash
nslookup example.com
```

Identify:

```text
A Record
AAAA Record
NS Record
```

---

## Lab 4 — HTTP

Run:

```bash
curl -I https://example.com
```

Then:

```bash
curl -v https://example.com
```

Observe:

```text
DNS Resolution
Connection
TLS
HTTP Request
HTTP Response
```

---

## Lab 5 — Listening Ports

Run:

```bash
ss -lntup
```

Identify:

```text
Port
Protocol
Process
Listening Address
```

---

# 💼 Interview Questions

- **What is computer networking?**  
  Computer networking is the communication of data between connected devices using networking protocols.

- **What is an IP address?**  
  An IP address identifies a network interface using the Internet Protocol addressing system.

- **What is the difference between IPv4 and IPv6?**  
  IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses and provides a much larger address space.

- **What is the OSI model?**  
  The OSI model is a seven-layer conceptual framework used to understand network communication.

- **What are the seven OSI layers?**  
  Application, Presentation, Session, Transport, Network, Data Link, and Physical.

- **What is the TCP/IP model?**  
  The TCP/IP model is the practical networking architecture used by Internet communication and is commonly represented using Application, Transport, Internet, and Network Access layers.

- **What is subnetting?**  
  Subnetting divides a larger network into smaller logical networks.

- **What is routing?**  
  Routing is the process of determining where packets should be forwarded to reach their destination.

- **What is NAT?**  
  NAT translates network addresses between different address spaces, commonly allowing private systems to communicate through public addresses.

- **What is DNS?**  
  DNS translates domain names into IP addresses and provides other DNS records.

- **What is DHCP?**  
  DHCP automatically provides network configuration such as IP address, subnet information, gateway, and DNS information to clients.

- **What is a port?**  
  A port identifies a transport-layer service endpoint associated with an IP address.

- **What is the difference between HTTP and HTTPS?**  
  HTTPS is HTTP protected using TLS, providing encryption and authentication-related security properties.

- **What is SSH?**  
  SSH is a secure protocol used for remote system access and command execution.

- **What does `ping` do?**  
  `ping` tests IP connectivity using ICMP echo messages.

- **What is `curl` used for?**  
  `curl` is used to communicate with network services and is especially useful for testing HTTP endpoints and APIs.

- **What is `dig` used for?**  
  `dig` is used to query and troubleshoot DNS records.

- **What is the difference between `ss` and `netstat`?**  
  Both can display network socket information, but `ss` is the modern tool generally preferred on Linux systems.

- **How would you troubleshoot a server that cannot access the Internet?**  
  Check the network interface, IP address, routing table, default gateway, external connectivity, DNS resolution, firewall rules, listening ports, and application protocol.

- **Why is networking important for DevOps?**  
  DevOps engineers work with servers, cloud infrastructure, containers, Kubernetes, load balancers, CI/CD systems, APIs, monitoring, and production applications—all of which depend heavily on networking.

---

# 🎯 Learning Outcome

After completing this topic, you should be able to:

- Explain basic networking concepts
- Identify common networking components
- Understand the OSI model
- Understand the TCP/IP model
- Explain IPv4 and IPv6
- Understand basic subnetting
- Explain routing
- Explain NAT
- Understand common network protocols
- Use basic Linux networking commands
- Perform basic connectivity tests
- Troubleshoot basic network problems
- Understand why networking is critical for DevOps

---

# 📚 Navigation

⬅️ Previous: **[Networking README](README.md)**

➡️ Next: **[02-OSI-Model.md](02-OSI-Model.md)**

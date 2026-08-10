# 🌐 Network Protocols

## 🎯 What Are We Learning?

So far we've learned:

```text
🌐 TCP/IP Model
      ↓
📍 IPv4
      ↓
📍 IPv6
      ↓
🧩 Subnetting
      ↓
🛣️ Routing
      ↓
🔄 NAT
```

Now comes one of the most important parts of networking:

> **Protocols**

Think of two people trying to communicate.

If one person speaks Marathi and the other speaks Japanese, communication becomes difficult.

Computers have the same problem.

They need agreed rules for:

```text
How to communicate
How to format data
How to establish connections
How to identify devices
How to transfer information
How to handle errors
```

These agreed rules are called:

> **Network Protocols**

---

# 🧠 What Is a Network Protocol?

A network protocol is a set of rules that defines how devices communicate over a network.

Think:

```text
👤 Person A
      ↕
📜 Common Rules
      ↕
👤 Person B
```

In networking:

```text
💻 Computer A
      ↕
🌐 Protocol
      ↕
🖥️ Computer B
```

---

# 🏠 Real-Life Example

Imagine ordering food.

You:

```text
📱 Open App
   ↓
🍔 Select Food
   ↓
💳 Pay
   ↓
📦 Order Confirmed
   ↓
🚴 Delivery
```

There are rules for every step.

Similarly, when you open:

```text
https://google.com
```

many protocols can be involved:

```text
DNS
 ↓
TCP
 ↓
TLS
 ↓
HTTPS
 ↓
IP
 ↓
Ethernet/Wi-Fi
```

Each protocol has a specific job.

---

# 🧩 Protocols Across the TCP/IP Model

Let's map some common protocols.

```text
┌─────────────────────────────────────┐
│ Application                         │
│ HTTP HTTPS DNS SSH DHCP SMTP FTP    │
├─────────────────────────────────────┤
│ Transport                           │
│ TCP UDP                             │
├─────────────────────────────────────┤
│ Internet                            │
│ IPv4 IPv6 ICMP                      │
├─────────────────────────────────────┤
│ Network Access                      │
│ Ethernet Wi-Fi ARP                  │
└─────────────────────────────────────┘
```

This isn't an exhaustive list, but these are some of the most useful protocols to recognize.

---

# 🌐 Protocol #1 — HTTP

HTTP stands for:

```text
Hypertext Transfer Protocol
```

It is used for communication between web clients and web servers.

Example:

```text
Browser
   ↓
HTTP Request
   ↓
Web Server
   ↓
HTTP Response
```

---

# 🏠 Real-Life Example

Think of visiting a restaurant.

You say:

> "Give me a pizza."

The restaurant responds:

> "Here is your pizza."

HTTP works similarly:

```text
Client:
"Give me /index.html"

       ↓

Server:
"Here is /index.html"
```

---

# 🧪 Try It

Run:

```bash
curl http://example.com
```

You are making an HTTP request.

Try:

```bash
curl -I http://example.com
```

You may see HTTP headers.

---

# 🔐 HTTP vs HTTPS

HTTPS means:

```text
HTTP over TLS
```

It provides encrypted communication between the client and server when TLS is correctly configured.

Think:

```text
HTTP
📨 Plain communication

HTTPS
🔐 Encrypted communication
```

Common HTTPS port:

```text
443
```

Common HTTP port:

```text
80
```

---

# 🔐 Protocol #2 — TLS

TLS stands for:

```text
Transport Layer Security
```

TLS provides security features such as:

```text
Encryption
Integrity
Authentication
```

A simplified HTTPS flow:

```text
Browser
   ↓
TLS
   ↓
HTTP
   ↓
TCP
   ↓
IP
```

TLS is not the same thing as HTTP.

Think:

```text
HTTP
"What are we saying?"

TLS
"How do we protect the conversation?"
```

---

# 🌐 Protocol #3 — DNS

DNS stands for:

```text
Domain Name System
```

DNS translates domain names into IP addresses and supports other types of name-related information.

Instead of remembering:

```text
142.250.x.x
```

you use:

```text
google.com
```

---

# 📱 Real-Life Example

Your phone contacts:

```text
"Mom"
   ↓
Actual Phone Number
```

DNS is conceptually similar:

```text
google.com
      ↓
IP Address
```

DNS acts like a naming system.

---

# 🧪 Try DNS

Run:

```bash
dig google.com
```

Or:

```bash
nslookup google.com
```

You can also query specific record types:

```bash
dig google.com A
```

```bash
dig google.com AAAA
```

Remember:

```text
A
 ↓
IPv4

AAAA
 ↓
IPv6
```

---

# 🚪 DNS Port

DNS commonly uses:

```text
UDP 53
```

It can also use:

```text
TCP 53
```

for situations such as larger responses and zone transfers.

So don't memorize:

> DNS = UDP only ❌

Better:

> DNS commonly uses UDP, but TCP is also used in specific cases.

---

# 🔑 Protocol #4 — SSH

SSH stands for:

```text
Secure Shell
```

SSH allows secure remote access to systems.

Example:

```bash
ssh user@server
```

Think:

```text
💻 Your Laptop
      ↓
🔐 SSH
      ↓
🖥️ Remote Linux Server
```

---

# 🏠 Real DevOps Example

You have an AWS EC2 instance:

```text
☁️ EC2
```

You need to manage it remotely.

You use:

```bash
ssh ubuntu@SERVER_IP
```

Now you have a remote shell.

SSH is extremely important for:

```text
Linux Administration
Cloud
DevOps
Automation
Troubleshooting
Server Management
```

---

# 🚪 SSH Port

Default SSH port:

```text
22
```

So:

```text
SSH
 ↓
TCP
 ↓
Port 22
```

---

# 📦 Protocol #5 — FTP

FTP stands for:

```text
File Transfer Protocol
```

It was designed for transferring files.

Example:

```text
💻 Client
   ↓
📦 File
   ↓
🖥️ FTP Server
```

FTP is an older protocol and does not provide encryption by itself.

---

# 🔐 SFTP

SFTP stands for:

```text
SSH File Transfer Protocol
```

Despite the similar name, SFTP is not simply "secure FTP."

It operates over SSH.

Typical port:

```text
22
```

Think:

```text
FTP
 ↓
Traditional file transfer

SFTP
 ↓
File transfer over SSH
```

---

# 📧 Protocol #6 — SMTP

SMTP stands for:

```text
Simple Mail Transfer Protocol
```

It is primarily used for sending and relaying email.

Think:

```text
📧 Email
   ↓
SMTP
   ↓
📨 Mail Server
```

Common ports include:

```text
25
587
465
```

The exact port depends on the email service and whether you're using relay, submission, or implicit TLS.

---

# 📥 Email Retrieval Protocols

Sending email and receiving email are different tasks.

Common retrieval protocols:

```text
IMAP
POP3
```

---

# 📬 IMAP

IMAP stands for:

```text
Internet Message Access Protocol
```

It allows clients to access and manage email stored on a mail server.

Common ports:

```text
143
993 → IMAPS
```

---

# 📥 POP3

POP3 stands for:

```text
Post Office Protocol version 3
```

It is another protocol for retrieving email.

Common ports:

```text
110
995 → POP3S
```

---

# 🧩 Protocol #7 — DHCP

DHCP stands for:

```text
Dynamic Host Configuration Protocol
```

It automatically provides network configuration to clients.

A DHCP server can provide things such as:

```text
IP Address
Subnet Mask / Prefix
Default Gateway
DNS Server
```

---

# 🏠 Real-Life Example

You connect your laptop to Wi-Fi.

You don't manually type:

```text
IP:
192.168.1.25

Gateway:
192.168.1.1

DNS:
192.168.1.1
```

Usually your network does this automatically.

DHCP helps provide that configuration.

---

# 🔄 DHCP Process

A commonly taught DHCP exchange is:

```text
D → Discover
O → Offer
R → Request
A → Acknowledge
```

Remember:

```text
DORA
```

Visual:

```text
💻 Client
   │
   │ Discover
   ↓
📡 DHCP Server
   │
   │ Offer
   ↓
💻 Client
   │
   │ Request
   ↓
📡 DHCP Server
   │
   │ ACK
   ↓
💻 Client
```

---

# 🌐 Protocol #8 — ICMP

ICMP stands for:

```text
Internet Control Message Protocol
```

It is used for network control, diagnostics, and error reporting.

The famous example:

```bash
ping
```

---

# 🧪 Ping

Run:

```bash
ping 8.8.8.8
```

Ping commonly uses:

```text
ICMP Echo Request
```

and:

```text
ICMP Echo Reply
```

Think:

```text
💻
"Are you there?"

      ↓

🖥️
"Yes, I'm here."
```

---

# ⚠️ Important

Ping failing does **not automatically mean the destination is down**.

ICMP can be:

```text
Blocked
Filtered
Rate-limited
```

A server can be healthy while refusing ICMP echo requests.

This is an important troubleshooting lesson.

---

# 🧩 Protocol #9 — ARP

ARP stands for:

```text
Address Resolution Protocol
```

It is used in IPv4 local networks to discover the MAC address associated with an IPv4 address.

Example:

```text
IP:
192.168.1.20

      ↓ ARP

MAC:
AA:BB:CC:DD:EE:FF
```

Think:

> 📍 "I know the IP. What's the local network hardware address?"

---

# 🏠 Real-Life Example

Imagine you know someone's apartment number:

```text
Flat 204
```

But you need to know:

> "Which exact person/device should I hand this to?"

ARP helps resolve:

```text
IPv4 Address
      ↓
MAC Address
```

within the local IPv4 network.

---

# 🧪 Check Neighbor Information

Modern Linux uses neighbor discovery commands such as:

```bash
ip neigh
```

You may see:

```text
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

This gives you information about a local IPv4 neighbor.

---

# 🧠 ARP and IPv6

IPv6 does **not** use ARP.

Instead, IPv6 uses:

```text
Neighbor Discovery Protocol
```

which is part of:

```text
ICMPv6
```

This is an important IPv4 vs IPv6 difference.

---

# 🌐 Protocol #10 — NDP

NDP stands for:

```text
Neighbor Discovery Protocol
```

It is used by IPv6 for functions including:

```text
Neighbor discovery
Router discovery
Address resolution
Neighbor reachability
```

It uses:

```text
ICMPv6
```

---

# 🆚 ARP vs NDP

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address resolution | ARP | NDP |
| Underlying protocol | ARP | ICMPv6 |
| IP version | IPv4 | IPv6 |

Remember:

```text
IPv4 → ARP
IPv6 → NDP
```

---

# 🚚 Protocol #11 — TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP provides:

```text
Reliable delivery
Ordered delivery
Retransmission
Flow control
Connection-oriented communication
```

Common applications:

```text
HTTPS
SSH
HTTP
```

---

# 🏎️ Protocol #12 — UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP is:

```text
Connectionless
Low overhead
No built-in retransmission
No built-in ordering
```

Common uses include:

```text
DNS
Real-time applications
Streaming/voice/video applications
```

The exact protocol used by an application depends on its design.

---

# 🆚 TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Built-in | No built-in reliability |
| Ordering | Yes | No built-in ordering |
| Retransmission | Yes | No |
| Overhead | Higher | Lower |
| Common Examples | HTTPS, SSH | DNS, real-time traffic |

---

# 🧠 Protocol #13 — IP

We've already learned:

```text
IPv4
IPv6
```

IP is responsible for logical addressing and routing packets between networks.

Think:

```text
📍 Source
   ↓
📦 Packet
   ↓
📍 Destination
```

---

# 🧩 Putting Everything Together

Let's say you type:

```text
https://example.com
```

A simplified sequence could be:

```text
1️⃣ DNS
   ↓
Find IP address

2️⃣ TCP
   ↓
Establish transport connection

3️⃣ TLS
   ↓
Secure the connection

4️⃣ HTTP
   ↓
Exchange web requests/responses

5️⃣ IP
   ↓
Route packets

6️⃣ Ethernet/Wi-Fi
   ↓
Move data across the local link
```

This is where everything you've learned starts connecting.

🔥 **Networking isn't a collection of random commands.**

It's a system.

---

# 🌐 Protocol Stack Example

For HTTPS over IPv4:

```text
Application
     │
     ├── HTTP
     └── TLS
     │
     ↓
Transport
     │
     └── TCP
     │
     ↓
Internet
     │
     └── IPv4
     │
     ↓
Network Access
     │
     └── Ethernet / Wi-Fi
```

For DNS:

```text
Application
     │
     └── DNS
     │
     ↓
Transport
     │
     └── UDP/TCP
     │
     ↓
Internet
     │
     └── IPv4/IPv6
```

---

# 🔢 Ports

Protocols often work with ports.

Think:

```text
IP Address
   ↓
🏢 Building

Port
   ↓
🚪 Door
```

Example:

```text
192.168.1.10:22
```

means:

```text
IP:
192.168.1.10

Port:
22
```

---

# 🔢 Common Ports You Should Know

| Protocol / Service | Port | Transport |
|---|---:|---|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| SSH | 22 | TCP |
| DNS | 53 | UDP/TCP |
| DHCP Server | 67 | UDP |
| DHCP Client | 68 | UDP |
| FTP | 21 | TCP |
| SMTP | 25 | TCP |
| SMTP Submission | 587 | TCP |
| IMAP | 143 | TCP |
| IMAPS | 993 | TCP |
| POP3 | 110 | TCP |
| POP3S | 995 | TCP |

> These are common/default ports, not absolute requirements. Applications can be configured to use different ports.

---

# 🎮 Protocol Matching Challenge

Match these:

```text
HTTP
HTTPS
DNS
SSH
DHCP
ICMP
ARP
TCP
UDP
SMTP
```

with:

```text
A. Secure remote access
B. Name resolution
C. Web communication
D. Automatic network configuration
E. Reliable transport
F. Email sending/relay
G. Diagnostic/control messaging
H. Local IPv4 address-to-MAC resolution
I. Secure web communication
J. Connectionless transport
```

### Answers

```text
HTTP  → C
HTTPS → I
DNS   → B
SSH   → A
DHCP  → D
ICMP  → G
ARP   → H
TCP   → E
UDP   → J
SMTP  → F
```

---

# 🎮 Port Challenge

Identify the protocol/service.

```text
22
53
80
443
25
```

### Answer

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
25  → SMTP
```

---

# 🧪 Hands-on Lab

Now let's investigate real protocols from your Linux machine.

---

## Mission 1 — DNS

Run:

```bash
dig google.com
```

Then:

```bash
dig google.com A
```

Then:

```bash
dig google.com AAAA
```

Identify:

```text
A record:
AAAA record:
```

---

# Mission 2 — HTTP

Run:

```bash
curl -I http://example.com
```

Look for:

```text
HTTP status
Server
Content-Type
```

---

# Mission 3 — HTTPS

Run:

```bash
curl -I https://example.com
```

Compare:

```text
HTTP
vs
HTTPS
```

Think:

> What security difference does TLS provide?

---

# Mission 4 — SSH

Check whether SSH is listening:

```bash
ss -lnt | grep :22
```

If nothing appears, that's okay.

Your machine may simply not be running an SSH server.

Don't install one just for this exercise.

---

# Mission 5 — ICMP

Run:

```bash
ping 127.0.0.1
```

Then:

```bash
ping 8.8.8.8
```

Think:

```text
What protocol is ping using?
```

Answer:

```text
ICMP
```

---

# Mission 6 — ARP / Neighbor Discovery

Run:

```bash
ip neigh
```

Look for local neighbor information.

If your environment has no entries, that's okay.

---

# Mission 7 — Listening Services

Run:

```bash
ss -lntup
```

Try to identify:

```text
Protocol:
Port:
Process:
```

Example:

```text
TCP
22
sshd
```

---

# 🔎 Mission 8 — See the Whole Journey

Run:

```bash
curl -I https://example.com
```

Think about everything involved:

```text
DNS
 ↓
IP
 ↓
TCP
 ↓
TLS
 ↓
HTTP
```

You're now connecting the previous chapters together.

---

# ☁️ Protocols in AWS

AWS networking uses these protocols constantly.

For example:

```text
🌍 User
   ↓
HTTPS :443
   ↓
⚖️ Load Balancer
   ↓
HTTP/HTTPS
   ↓
🖥️ Application
   ↓
TCP
   ↓
🗄️ Database
```

Security Groups can control traffic based on:

```text
Protocol
Port
Source
Destination
```

Example:

```text
Allow TCP
Port 443
Source: Internet
```

means:

```text
🌍 Internet
      ↓
TCP :443
      ↓
Application
```

---

# 🐳 Protocols in Docker

Suppose:

```text
Browser
   ↓
localhost:8080
   ↓
Docker
   ↓
Container:80
   ↓
Nginx
```

You need to understand:

```text
IP
Port
TCP
HTTP
NAT
```

For example:

```bash
docker run -p 8080:80 nginx
```

means:

```text
Host Port 8080
      ↓
Container Port 80
```

---

# ☸️ Protocols in Kubernetes

Imagine:

```text
User
 ↓
HTTPS
 ↓
Ingress
 ↓
Service
 ↓
Pod
```

You'll encounter:

```text
HTTP
HTTPS
TCP
UDP
DNS
TLS
IP
```

And Kubernetes adds:

```text
Service Discovery
Load Balancing
Network Policies
Ingress
CNI
```

Understanding basic protocols first makes these much easier.

---

# 🚨 Real DevOps Troubleshooting

Imagine:

```text
Application is running.
```

But users say:

> "The website isn't opening."

Don't immediately restart the server. 😂

Investigate layer by layer.

---

## Step 1 — DNS

```bash
dig example.com
```

Question:

```text
Does the name resolve?
```

---

## Step 2 — IP Connectivity

```bash
ping SERVER_IP
```

Remember:

> Ping failure does not automatically mean the server is down.

---

## Step 3 — Route

```bash
ip route get SERVER_IP
```

Question:

```text
Is traffic going through the expected route?
```

---

## Step 4 — Port

```bash
ss -lntup
```

Question:

```text
Is the service listening?
```

---

## Step 5 — HTTP/HTTPS

```bash
curl -I https://example.com
```

Question:

```text
Does the application respond?
```

---

## Step 6 — TLS

If HTTPS fails:

```bash
curl -v https://example.com
```

Investigate:

```text
TLS handshake
Certificate
Protocol
Connection
```

---

# 🧠 Troubleshooting Flow

Remember:

```text
🌐 DNS
   ↓
📍 IP
   ↓
🛣️ Routing
   ↓
🚪 Port
   ↓
🔐 TLS
   ↓
🌐 HTTP
   ↓
🖥️ Application
```

This is much better than:

```text
"Restart everything." 😂
```

---

# 🧠 Protocol Cheat Sheet

```text
HTTP
→ Web

HTTPS
→ Secure Web

DNS
→ Name → IP

SSH
→ Secure remote access

DHCP
→ Automatic network configuration

TCP
→ Reliable transport

UDP
→ Connectionless transport

ICMP
→ Diagnostics/control

ARP
→ IPv4 → MAC on local network

NDP
→ IPv6 neighbor discovery

SMTP
→ Send/relay email

IMAP
→ Access/manage email

POP3
→ Retrieve email

FTP
→ File transfer

SFTP
→ File transfer over SSH

IP
→ Addressing + routing
```

---

# 🧠 The Big Picture

You should now be able to visualize:

```text
                     🌍 Internet
                          │
                          ↓
                       DNS
                          │
                     "Where?"
                          ↓
                     IP Address
                          │
                          ↓
                       Routing
                          │
                          ↓
                      TCP/UDP
                          │
                       "How?"
                          ↓
                      Port 443
                          │
                          ↓
                        TLS
                          │
                       "Secure"
                          ↓
                       HTTP
                          │
                       "Data"
                          ↓
                    🖥️ Application
```

That's how the pieces connect.

---

# 💼 Interview Corner

### Q: What is a network protocol?

> A network protocol is a defined set of rules that allows networked systems to communicate.

---

### Q: What is HTTP?

> HTTP is an application-layer protocol used for communication between web clients and servers.

---

### Q: What is HTTPS?

> HTTPS is HTTP protected using TLS.

---

### Q: What is DNS?

> DNS is a distributed naming system used to resolve domain names and provide other DNS information such as IP addresses.

---

### Q: What is DHCP?

> DHCP automatically provides network configuration information such as IP addresses, gateways, and DNS servers to clients.

---

### Q: What is SSH?

> SSH is a secure protocol used for remote access and administration of systems.

---

### Q: What is ICMP?

> ICMP is used for network control, diagnostics, and error reporting.

---

### Q: What is ARP?

> ARP resolves IPv4 addresses to MAC addresses on a local network.

---

### Q: Does IPv6 use ARP?

```text
No ❌
```

IPv6 uses:

```text
NDP
```

through:

```text
ICMPv6
```

---

### Q: What is the difference between TCP and UDP?

> TCP provides connection-oriented, reliable, ordered transport, while UDP provides connectionless transport without TCP's built-in reliability and ordering mechanisms.

---

### Q: What port does HTTPS normally use?

```text
443
```

---

### Q: What port does SSH normally use?

```text
22
```

---

### Q: What port does DNS normally use?

```text
53
```

DNS can use both:

```text
UDP
TCP
```

---

### Q: What is DORA?

```text
Discover
Offer
Request
Acknowledge
```

It's the commonly taught DHCP exchange sequence.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain what a network protocol is
- [ ] Explain HTTP
- [ ] Explain HTTPS
- [ ] Explain TLS
- [ ] Explain DNS
- [ ] Explain SSH
- [ ] Explain DHCP
- [ ] Explain ICMP
- [ ] Explain ARP
- [ ] Explain NDP
- [ ] Explain SMTP
- [ ] Explain IMAP
- [ ] Explain POP3
- [ ] Explain FTP
- [ ] Explain SFTP
- [ ] Explain TCP
- [ ] Explain UDP
- [ ] Explain ports
- [ ] Know common protocol ports
- [ ] Explain A vs AAAA records
- [ ] Explain DORA
- [ ] Explain IPv4 ARP vs IPv6 NDP
- [ ] Use `curl`
- [ ] Use `dig`
- [ ] Use `ping`
- [ ] Use `ip neigh`
- [ ] Use `ss`
- [ ] Troubleshoot a basic web connectivity problem
- [ ] Explain how protocols appear in AWS
- [ ] Explain how protocols appear in Docker
- [ ] Explain how protocols appear in Kubernetes

---

# 🎯 Mini Project

## 🚀 Trace a Web Request

Pick:

```text
https://example.com
```

Create your own diagram:

```text
💻 Your Laptop
      │
      ↓
     DNS
      │
      ↓
   IP Address
      │
      ↓
    Routing
      │
      ↓
     TCP
      │
      ↓
     TLS
      │
      ↓
    HTTPS
      │
      ↓
🖥️ Web Server
```

Then answer:

```text
1. Which protocol resolves the domain name?

2. Which record provides an IPv4 address?

3. Which record provides an IPv6 address?

4. Which transport protocol is commonly used by HTTPS?

5. What port does HTTPS normally use?

6. What protocol provides encryption for HTTPS?

7. Which command can inspect DNS?

8. Which command can test connectivity?

9. Which command can inspect listening ports?

10. Which command can show Linux's route to the destination?
```

### Expected tools:

```bash
dig
ping
ss
ip route get
```

---

# 🔥 DevOps Connection

This topic is a major turning point.

Before this, networking looked like:

```text
IP
Subnet
Router
NAT
```

Now you can see how applications actually use the network:

```text
DNS
 ↓
IP
 ↓
Routing
 ↓
TCP/UDP
 ↓
Port
 ↓
TLS
 ↓
HTTP
 ↓
Application
```

This exact knowledge will come back when you work with:

```text
☁️ AWS
🐳 Docker
☸️ Kubernetes
🔧 CI/CD
🌐 APIs
🔐 Security
📊 Monitoring
🚨 Production Troubleshooting
```

When an application says:

> **"Connection refused"**

you should start thinking:

```text
Is the service listening?
        ↓
Is the port correct?
        ↓
Is the route correct?
        ↓
Is the firewall allowing it?
        ↓
Is DNS correct?
        ↓
Is the application healthy?
```

That's the mindset we're building. 🔥

---

# 📚 Navigation

⬅️ Previous: **[08-NAT.md](08-NAT.md)**

➡️ Next: **[10-DNS.md](10-DNS.md)**

🏠 Networking Phase: **[README.md](README.md)**

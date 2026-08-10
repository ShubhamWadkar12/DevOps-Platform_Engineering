# 🧪 Networking Hands-on Labs

## 🎯 What Are We Doing?

Enough theory. 😎

Now we're going to **touch the network**.

The goal of these labs is to turn:

```text
📚 Theory
   ↓
🧠 Understanding
   ↓
💻 Commands
   ↓
🧪 Experiments
   ↓
🔥 Troubleshooting Skills
```

into practical DevOps networking skills.

> **Rule:** Don't just copy commands. Run them, observe the output, and write down what you learned.

---

# 🧰 Lab Environment

These labs can be performed mainly using:

```text
💻 Windows
   ↓
🐧 WSL / Ubuntu
   ↓
Terminal
```

Recommended environment:

```text
Ubuntu 24.04 LTS
```

Check your Linux version:

```bash
cat /etc/os-release
```

Check kernel:

```bash
uname -r
```

---

# 🗺️ Labs Roadmap

| Lab | Topic | Difficulty |
|---|---|---|
| 01 | Network Interface Discovery | 🟢 Easy |
| 02 | IP Address Investigation | 🟢 Easy |
| 03 | Routing Table | 🟢 Easy |
| 04 | DNS Investigation | 🟢 Easy |
| 05 | Ping & Connectivity | 🟢 Easy |
| 06 | Port Testing | 🟢 Easy |
| 07 | Local Web Server | 🟢 Easy |
| 08 | HTTP Troubleshooting | 🟡 Medium |
| 09 | Network Path Analysis | 🟡 Medium |
| 10 | Listening Ports | 🟡 Medium |
| 11 | Linux Firewall | 🟡 Medium |
| 12 | Packet Capture | 🔴 Advanced |
| 13 | Network Troubleshooting Challenge | 🔴 Advanced |
| 14 | AWS VPC Design Lab | 🔴 Advanced |
| 15 | Final Networking Project | 🔴 Advanced |

---

# 🧪 Lab 01 — Network Interface Discovery

## 🎯 Objective

Understand:

```text
Network Interfaces
IPv4 Addresses
IPv6 Addresses
MAC Addresses
Loopback
```

---

## Step 1 — View Interfaces

Run:

```bash
ip link
```

You should see interfaces such as:

```text
lo
eth0
```

or another interface name depending on your environment.

---

## Step 2 — View IP Addresses

Run:

```bash
ip addr
```

Look for:

```text
inet
inet6
```

---

## Step 3 — Identify Loopback

Find:

```text
lo
```

Usually:

```text
127.0.0.1
```

This is the IPv4 loopback address.

---

## 🧠 Understand

```text
127.0.0.1
     ↓
Your own machine
```

It doesn't represent another machine on your network.

---

## 📝 Your Notes

Record:

```text
Interface:
IPv4:
IPv6:
MAC:
Loopback:
```

---

# 🧪 Lab 02 — IP Address Investigation

## 🎯 Objective

Understand your machine's network addressing.

Run:

```bash
ip addr
```

Find your IPv4 address.

Example:

```text
192.168.1.20/24
```

Break it down:

```text
IP:
192.168.1.20

Prefix:
24
```

---

## 🧠 Question

What does `/24` mean?

It means:

```text
24 network bits
8 host bits
```

The traditional subnet mask is:

```text
255.255.255.0
```

---

## 📝 Record

```text
IPv4:
CIDR:
Subnet Mask:
Interface:
```

---

# 🧪 Lab 03 — Routing Table

## 🎯 Objective

Understand how Linux decides where traffic goes.

Run:

```bash
ip route
```

You may see something similar to:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link
```

---

# 🧠 Understand

The:

```text
default
```

route is used when a more specific route isn't available.

Example:

```text
Destination:
8.8.8.8

No specific route
     ↓
Default Route
     ↓
Gateway
```

---

## Step 2 — Test a Specific Destination

Run:

```bash
ip route get 8.8.8.8
```

Observe:

```text
Gateway
Interface
Source IP
```

---

## 🎮 Challenge

Run:

```bash
ip route get 1.1.1.1
```

Then answer:

```text
Which interface is used?

Which source IP is selected?

Which gateway is used?
```

---

# 🧪 Lab 04 — DNS Investigation

## 🎯 Objective

Understand how domain names become IP addresses.

---

## Step 1

Run:

```bash
dig google.com
```

Look for:

```text
ANSWER SECTION
```

---

## Step 2

Run:

```bash
dig +short google.com
```

This gives a more concise answer.

---

## Step 3

Run:

```bash
nslookup google.com
```

Compare the result.

---

## Step 4

Run:

```bash
getent hosts google.com
```

---

# 🧠 Understand

The basic process:

```text
google.com
     ↓
DNS
     ↓
IP Address
     ↓
Server
```

---

# 🔎 Check Your DNS Configuration

Run:

```bash
cat /etc/resolv.conf
```

Identify the configured DNS resolver(s).

---

# 🎮 Challenge

Run:

```bash
dig google.com
```

Then:

```bash
dig example.com
```

Compare:

```text
IP addresses
Response time
DNS server
```

---

# 🧪 Lab 05 — Ping & Connectivity

## 🎯 Objective

Understand basic IP connectivity and ICMP.

Run:

```bash
ping -c 4 8.8.8.8
```

Observe:

```text
Packets transmitted
Packets received
Packet loss
Latency
```

---

## Step 2

Run:

```bash
ping -c 4 google.com
```

Now you're testing:

```text
DNS resolution
+
ICMP connectivity
```

---

# 🧠 Important

A successful ping doesn't mean:

```text
HTTPS works
SSH works
Database works
Application works
```

It only tells you that the ICMP test received responses.

---

# 🎮 Challenge

Compare:

```bash
ping -c 4 8.8.8.8
```

and:

```bash
ping -c 4 google.com
```

If the first works but the second doesn't:

```text
What could be wrong?
```

Expected area:

```text
DNS
```

---

# 🧪 Lab 06 — Port Testing

## 🎯 Objective

Test whether a TCP port is reachable.

---

## Step 1

Test HTTPS:

```bash
nc -vz google.com 443
```

---

## Step 2

Test another port:

```bash
nc -vz google.com 22
```

The result may vary depending on the destination and its network/security configuration.

---

# 🧠 Important

A port test asks:

> "Can I establish a connection to this service endpoint?"

It is more application-relevant than simply using ping.

---

# 🧪 Lab 07 — Build Your Own Web Server

## 🎯 Objective

Create a local service and troubleshoot it yourself.

---

## Step 1 — Create Lab Directory

```bash
mkdir -p ~/network-lab
cd ~/network-lab
```

---

## Step 2 — Create a Page

```bash
echo "Hello from my Networking Lab!" > index.html
```

---

## Step 3 — Start Web Server

Run:

```bash
python3 -m http.server 8080
```

You should see something similar to:

```text
Serving HTTP on 0.0.0.0 port 8080
```

---

# 🧪 Step 4 — Test It

Open another terminal.

Run:

```bash
curl http://127.0.0.1:8080
```

Expected:

```text
Hello from my Networking Lab!
```

🎉 You just created your own web service.

---

# 🔎 Step 5 — Find the Listening Port

Run:

```bash
ss -lntup
```

Look for:

```text
8080
```

---

# 🧠 Architecture

```text
curl
 ↓
127.0.0.1:8080
 ↓
Python HTTP Server
 ↓
index.html
```

---

# 🧪 Lab 08 — HTTP Troubleshooting

Keep the Python server running:

```bash
python3 -m http.server 8080
```

Now test:

```bash
curl -v http://127.0.0.1:8080
```

Observe:

```text
TCP connection
HTTP request
HTTP response
Status code
Headers
```

---

# 🧠 Understand the Flow

```text
Client
  ↓
TCP Connection
  ↓
HTTP Request
  ↓
Web Server
  ↓
HTTP Response
```

---

# 🎮 Challenge

Try:

```bash
curl -v http://127.0.0.1:9999
```

What happens?

There is probably no service listening on:

```text
9999
```

Compare this with:

```bash
curl -v http://127.0.0.1:8080
```

---

# 🧪 Lab 09 — Network Path Analysis

## 🎯 Objective

Understand the path packets take toward a destination.

Run:

```bash
traceroute google.com
```

If `traceroute` isn't installed:

```bash
sudo apt update
sudo apt install traceroute
```

Then:

```bash
traceroute google.com
```

---

# Alternative

You can also try:

```bash
tracepath google.com
```

---

# 🧠 Understand

Conceptually:

```text
Your Computer
      ↓
Router
      ↓
ISP
      ↓
Internet
      ↓
Google Network
      ↓
Destination
```

---

# ⚠️ Important

Traceroute output isn't always complete.

You may see:

```text
*
*
*
```

This can happen because routers may:

```text
Block probes
Rate-limit responses
Not respond to traceroute
```

Don't automatically assume the network is broken.

---

# 🧪 Lab 10 — Listening Ports

## 🎯 Objective

Understand what services are accepting connections on your Linux machine.

Run:

```bash
ss -lntup
```

---

# 🧠 Understand the Options

```text
-l
→ listening

-n
→ don't resolve names

-t
→ TCP

-u
→ UDP

-p
→ process information
```

---

# 🔎 Find a Specific Port

```bash
ss -lntup | grep 8080
```

If your Python server is running, you should find it.

---

# 🎮 Challenge

Start:

```bash
python3 -m http.server 8080
```

Then:

```bash
ss -lntup | grep 8080
```

Now stop the server with:

```text
CTRL + C
```

Run again:

```bash
ss -lntup | grep 8080
```

What changed?

---

# 🧪 Lab 11 — Linux Firewall Investigation

## 🎯 Objective

Understand how host-level firewall rules can affect traffic.

First identify what your system uses.

Try:

```bash
sudo ufw status
```

If UFW is not being used, inspect nftables:

```bash
sudo nft list ruleset
```

On systems using legacy iptables:

```bash
sudo iptables -L
```

---

# ⚠️ IMPORTANT

Do NOT randomly execute firewall commands.

Especially avoid experimenting with:

```text
Production servers
Remote servers
SSH connections
Cloud instances
```

A firewall mistake can lock you out.

The goal of this lab is initially:

```text
Observe
 ↓
Understand
 ↓
Then modify
```

---

# 🧪 Lab 12 — Packet Capture with tcpdump

## 🎯 Objective

See actual packets moving through the interface.

Install if required:

```bash
sudo apt update
sudo apt install tcpdump
```

---

# Step 1

Run:

```bash
sudo tcpdump -i any
```

You'll start seeing network packets.

Stop with:

```text
CTRL + C
```

---

# Step 2 — Capture Port 8080

Start your web server:

```bash
python3 -m http.server 8080
```

In another terminal:

```bash
sudo tcpdump -i any port 8080
```

Then:

```bash
curl http://127.0.0.1:8080
```

Watch the packets.

---

# 🧠 What Are You Seeing?

Conceptually:

```text
Client
  ↓
TCP SYN
  ↓
Server

Server
  ↓
TCP SYN-ACK
  ↓
Client

Client
  ↓
TCP ACK
  ↓
Server
```

Then:

```text
HTTP Request
      ↓
HTTP Response
```

---

# 🧪 Lab 13 — TCP Three-Way Handshake

## 🎯 Objective

Understand TCP connection establishment.

Use:

```bash
sudo tcpdump -i any port 8080
```

Then:

```bash
curl http://127.0.0.1:8080
```

Look for:

```text
SYN
SYN-ACK
ACK
```

---

# 🧠 Remember

```text
Client                 Server

SYN ─────────────────→

    ←──────────────── SYN-ACK

ACK ─────────────────→

Connection Established
```

---

# 🧪 Lab 14 — Localhost vs Network Interface

## 🎯 Objective

Understand the difference between:

```text
127.0.0.1
```

and:

```text
0.0.0.0
```

Start:

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

Test:

```bash
curl http://127.0.0.1:8080
```

It should work locally.

---

# 🧠 Understand

```text
127.0.0.1
```

means:

```text
Loopback only
```

A service bound only to loopback isn't listening for connections through the machine's other network interfaces.

---

# 🧪 Lab 15 — Bind to All IPv4 Interfaces

Stop the server:

```text
CTRL + C
```

Start:

```bash
python3 -m http.server 8080 --bind 0.0.0.0
```

Now inspect:

```bash
ss -lntup | grep 8080
```

You should see the service listening on an address representing all IPv4 interfaces.

---

# 🧠 Difference

```text
127.0.0.1:8080
```

means:

```text
Only local loopback
```

Whereas:

```text
0.0.0.0:8080
```

means:

```text
Listen on all IPv4 interfaces
```

assuming the host firewall/network allows access.

---

# 🧪 Lab 16 — DNS + HTTP + TCP

Now combine everything.

Run:

```bash
curl -v https://example.com
```

Think through the complete process:

```text
Hostname
   ↓
DNS
   ↓
IP Address
   ↓
Routing
   ↓
TCP 443
   ↓
TLS
   ↓
HTTP
   ↓
Response
```

This is an extremely important DevOps mental model.

---

# 🧪 Lab 17 — Build a Troubleshooting Checklist

Imagine:

```text
Application cannot reach database.
```

Use this order:

```text
1️⃣ DNS
2️⃣ IP
3️⃣ Route
4️⃣ Connectivity
5️⃣ Port
6️⃣ Firewall
7️⃣ Security Group
8️⃣ NACL
9️⃣ Service
🔟 Application
```

---

# 🧪 Example

Application:

```text
10.0.2.10
```

Database:

```text
10.0.3.10
```

Database port:

```text
5432
```

Test:

```bash
ping 10.0.3.10
```

Then:

```bash
nc -vz 10.0.3.10 5432
```

Then investigate:

```text
Route
Security Group
NACL
Firewall
Database
```

---

# 🎮 Lab 18 — Break It Yourself

This is one of the best ways to learn troubleshooting.

Start:

```bash
python3 -m http.server 8080
```

Confirm:

```bash
curl http://127.0.0.1:8080
```

works.

Then stop the server:

```text
CTRL + C
```

Run:

```bash
curl http://127.0.0.1:8080
```

Now troubleshoot.

---

# 🧠 What Changed?

Before:

```text
Service
 ↓
Listening
 ↓
TCP 8080
 ↓
HTTP
 ↓
✅
```

After:

```text
Service
 ↓
❌ Not running
```

The network itself wasn't necessarily broken.

The application/service was unavailable.

---

# 🎮 Lab 19 — Wrong Port Challenge

Start:

```bash
python3 -m http.server 8080
```

Correct:

```bash
curl http://127.0.0.1:8080
```

Wrong:

```bash
curl http://127.0.0.1:8081
```

Compare the errors.

Question:

> Is the server running?

Yes.

Question:

> Is anything listening on 8081?

Probably not.

---

# 🎮 Lab 20 — DNS Failure Simulation

Run:

```bash
curl http://this-domain-should-not-exist-123456.example
```

You should get a DNS-related failure.

Your job:

```text
Identify the error
Identify the layer
Explain why the request never reached the application
```

Expected:

```text
DNS
```

---

# 🧪 Lab 21 — Application Layer Test

Start:

```bash
python3 -m http.server 8080
```

Run:

```bash
curl -I http://127.0.0.1:8080
```

You should see an HTTP response such as:

```text
HTTP/1.0 200 OK
```

---

# 🧠 Layered View

You just tested:

```text
Application
   ↓
HTTP
   ↓
TCP
   ↓
IP
   ↓
Network Interface
```

This is the same layered thinking you'll use with:

```text
Docker
Kubernetes
AWS
Load Balancers
Microservices
```

---

# 🧪 Lab 22 — Network Information Collection

Create a file:

```bash
mkdir -p ~/network-lab
cd ~/network-lab
touch network-report.txt
```

Run:

```bash
ip addr
```

Save the output:

```bash
ip addr > network-report.txt
```

Append routing:

```bash
ip route >> network-report.txt
```

Append DNS:

```bash
cat /etc/resolv.conf >> network-report.txt
```

View:

```bash
cat network-report.txt
```

---

# 🧠 Your Network Report

Your file should contain:

```text
Network Interfaces
IPv4 Addresses
IPv6 Addresses
Routing Table
DNS Configuration
```

---

# 🧪 Lab 23 — Create a Network Diagnostic Script

Create:

```bash
nano network-diagnostics.sh
```

Add:

```bash
#!/bin/bash

echo "=============================="
echo "   NETWORK DIAGNOSTICS"
echo "=============================="

echo ""
echo "📡 IP Addresses"
ip addr

echo ""
echo "🛣️ Routing Table"
ip route

echo ""
echo "🌐 DNS Configuration"
cat /etc/resolv.conf

echo ""
echo "👂 Listening Ports"
ss -lntup

echo ""
echo "=============================="
echo "Diagnostics Complete"
echo "=============================="
```

---

# 🧪 Make It Executable

```bash
chmod +x network-diagnostics.sh
```

Run:

```bash
./network-diagnostics.sh
```

---

# 🔥 DevOps Connection

This is your first tiny piece of:

> **Infrastructure automation**

Instead of manually running:

```text
ip addr
ip route
ss
cat /etc/resolv.conf
```

you created:

```text
network-diagnostics.sh
```

Later you'll automate much bigger tasks with:

```text
Shell
Python
Ansible
Terraform
CI/CD
```

---

# 🧪 Lab 24 — Network Troubleshooting Script

Create:

```bash
nano troubleshoot.sh
```

Add:

```bash
#!/bin/bash

echo "=============================="
echo " Network Troubleshooting Tool"
echo "=============================="

echo ""
echo "📡 IP Information"
ip addr

echo ""
echo "🛣️ Routes"
ip route

echo ""
echo "🌐 DNS Test"
ping -c 2 google.com

echo ""
echo "🔎 DNS Resolution"
getent hosts google.com

echo ""
echo "🔐 HTTPS Connectivity"
curl -I --max-time 5 https://example.com

echo ""
echo "👂 Listening Ports"
ss -lntup

echo ""
echo "=============================="
echo " Done"
echo "=============================="
```

Make executable:

```bash
chmod +x troubleshoot.sh
```

Run:

```bash
./troubleshoot.sh
```

---

# ⚠️ Important

This script is for learning.

Production diagnostic scripts should:

```text
Handle errors
Use timeouts
Avoid leaking sensitive information
Log safely
Use controlled permissions
```

---

# 🧪 Lab 25 — AWS VPC Design

Now move from:

```text
🐧 Linux Networking
```

to:

```text
☁️ Cloud Networking
```

Design:

```text
VPC:
10.0.0.0/16
```

Subnets:

```text
Public:
10.0.1.0/24

Private App:
10.0.2.0/24

Private Database:
10.0.3.0/24
```

---

# 🏗️ Architecture

```text
                    ☁️ VPC
                 10.0.0.0/16
                       │
         ┌─────────────┼─────────────┐
         ↓             ↓             ↓
      🌐 Public     🔒 App        🗄️ DB
      10.0.1.0/24  10.0.2.0/24  10.0.3.0/24
         │             │             │
         ↓             ↓             ↓
        ALB           App           DB
```

---

# 🧠 Design Questions

Answer:

```text
1. Which subnet should be public?

2. Which should be private?

3. Which resource should face the Internet?

4. Which resource should access the database?

5. Should the database have a public IP?

6. Which Security Groups are required?

7. Which routes are required?
```

---

# 🧪 Lab 26 — VPC Peering Design

Design:

```text
VPC A
10.0.0.0/16

      🔗

VPC B
10.1.0.0/16
```

Routes:

```text
VPC A
10.1.0.0/16 → Peering

VPC B
10.0.0.0/16 → Peering
```

---

# 🎮 Challenge

Now change VPC B to:

```text
10.0.0.0/16
```

Question:

> What happens?

Answer:

```text
CIDR overlap ❌
```

---

# 🧪 Lab 27 — VPN Design

Design:

```text
🏢 On-Premises
192.168.0.0/16
        │
        🔐
        │
        ↓
☁️ AWS
10.0.0.0/16
```

Routes:

```text
On-Prem
10.0.0.0/16 → VPN

AWS
192.168.0.0/16 → VPN
```

---

# 🧠 Troubleshooting Challenge

VPN:

```text
UP ✅
```

But:

```text
Application → Database ❌
```

Investigate:

```text
Route
 ↓
Security Group
 ↓
NACL
 ↓
Firewall
 ↓
Database
 ↓
Return Route
```

---

# 🧪 Lab 28 — Final Troubleshooting Challenge

## 🚨 Scenario

You have:

```text
🌍 Internet
      ↓
⚖️ Load Balancer
      ↓
🖥️ Application
      ↓
🗄️ Database
```

Users report:

```text
Website is slow.
```

Your job is to investigate.

---

# 🔍 Investigation

Check:

```text
DNS
 ↓
Load Balancer
 ↓
Target Health
 ↓
Application
 ↓
Database
```

Useful tools:

```bash
dig
curl
nc
ss
ip route
systemctl
journalctl
tcpdump
```

---

# 🎮 Possible Root Causes

Your investigation could reveal:

```text
❌ DNS problem
❌ Route problem
❌ Security Group
❌ NACL
❌ Application crash
❌ Wrong port
❌ Database slow
❌ Load Balancer unhealthy targets
❌ High latency
❌ Network packet loss
```

Your task is to identify the actual cause using evidence.

---

# 🧪 Lab 29 — Final Networking Assessment

Without looking at previous notes, explain:

### 1️⃣ What happens when you type:

```text
https://example.com
```

Think:

```text
DNS
 ↓
IP
 ↓
Routing
 ↓
TCP
 ↓
TLS
 ↓
HTTP
 ↓
Response
```

---

### 2️⃣ What happens if DNS fails?

```text
Hostname
 ↓
❌ DNS
 ↓
No destination IP
 ↓
Request cannot proceed normally
```

---

### 3️⃣ What happens if routing fails?

```text
DNS
 ↓
IP
 ↓
❌ Route
 ↓
Traffic can't reach destination
```

---

### 4️⃣ What happens if port 443 is blocked?

```text
DNS ✅
IP ✅
Route ✅
TCP 443 ❌
HTTP ❌
```

---

### 5️⃣ What happens if the application crashes?

```text
DNS ✅
IP ✅
Route ✅
Port ❌ / service unavailable
Application ❌
```

---

# 🧠 Master Troubleshooting Model

Memorize the **concept**, not just the commands:

```text
                 🚨 APPLICATION PROBLEM
                          │
                          ↓
                     DNS Working?
                       /      \
                     NO        YES
                     ↓          ↓
                  Fix DNS     Correct IP?
                                │
                                ↓
                             Routing?
                              /    \
                            NO      YES
                            ↓        ↓
                         Fix Route  Port?
                                     / \
                                   NO   YES
                                   ↓     ↓
                              Firewall  Service?
                                        /    \
                                      NO      YES
                                      ↓        ↓
                                  Start/Fix  App?
                                               │
                                               ↓
                                             Logs
```

---

# 🏆 Final Hands-on Checklist

## Linux Networking

- [ ] `ip addr`
- [ ] `ip link`
- [ ] `ip route`
- [ ] `ip route get`
- [ ] `ping`
- [ ] `dig`
- [ ] `nslookup`
- [ ] `getent`
- [ ] `traceroute`
- [ ] `tracepath`
- [ ] `nc`
- [ ] `curl`
- [ ] `ss`
- [ ] `tcpdump`

---

## Concepts

- [ ] IP Address
- [ ] Subnet
- [ ] Gateway
- [ ] Routing
- [ ] DNS
- [ ] TCP
- [ ] UDP
- [ ] Ports
- [ ] HTTP
- [ ] HTTPS
- [ ] Firewall
- [ ] Security Group
- [ ] NACL
- [ ] VPC
- [ ] VPC Peering
- [ ] VPN
- [ ] Load Balancer
- [ ] Network Security

---

## Troubleshooting

- [ ] DNS failure
- [ ] Routing failure
- [ ] Port failure
- [ ] Firewall problem
- [ ] Security Group problem
- [ ] NACL problem
- [ ] Application problem
- [ ] Load Balancer problem
- [ ] VPN problem
- [ ] VPC Peering problem
- [ ] TCP troubleshooting
- [ ] Packet capture
- [ ] Log analysis

---

# 🏆 Final Challenge — Become the Network Detective

Imagine someone tells you:

> 🚨 "The application cannot connect to the database."

You are NOT allowed to randomly change anything.

You must answer:

```text
Who is connecting?
        ↓
What are they connecting to?
        ↓
Which IP?
        ↓
Which port?
        ↓
Does DNS work?
        ↓
Is there a route?
        ↓
Can packets reach the destination?
        ↓
Is the port open?
        ↓
Is the firewall allowing it?
        ↓
Is the Security Group allowing it?
        ↓
Is the NACL allowing it?
        ↓
Is the service listening?
        ↓
Is the application working?
        ↓
What do the logs say?
```

That is the mindset of a real DevOps Engineer. 🔥

---

# 🎯 Final Mini Project

## 🚀 Build a Network Diagnostics Toolkit

Create this structure:

```text
networking-toolkit/
│
├── README.md
│
├── network-info.sh
├── dns-check.sh
├── connectivity-check.sh
├── port-check.sh
├── service-check.sh
└── network-diagnostics.sh
```

---

## `network-info.sh`

Should collect:

```text
IP addresses
Interfaces
Routes
```

---

## `dns-check.sh`

Should test:

```text
DNS resolution
```

---

## `connectivity-check.sh`

Should test:

```text
Ping
```

---

## `port-check.sh`

Should test:

```text
TCP connectivity
```

---

## `service-check.sh`

Should show:

```text
Listening ports
Running services
```

---

## `network-diagnostics.sh`

Combine everything:

```text
Network Info
     ↓
DNS
     ↓
Connectivity
     ↓
Ports
     ↓
Services
     ↓
Summary
```

---

# 💼 DevOps Connection

These labs are not just Linux exercises.

You're building the foundation for:

```text
🐧 Linux
   ↓
🌐 Networking
   ↓
☁️ AWS
   ↓
🐳 Docker Networking
   ↓
☸️ Kubernetes Networking
   ↓
🏗️ Terraform
   ↓
🚀 CI/CD
   ↓
📊 Monitoring
   ↓
🔐 DevSecOps
```

When a Kubernetes pod can't reach a database:

```text
DNS
 ↓
Service
 ↓
ClusterIP
 ↓
Network Policy
 ↓
Pod
 ↓
Container
 ↓
Application
```

When an EC2 instance can't reach another service:

```text
Route Table
 ↓
Security Group
 ↓
NACL
 ↓
OS Firewall
 ↓
Port
 ↓
Application
```

When a production website returns `504`:

```text
DNS
 ↓
Load Balancer
 ↓
Target Health
 ↓
Network
 ↓
Application
 ↓
Database
```

Same troubleshooting mindset.

Different infrastructure.

---

# 🧠 The One Rule to Remember

> **Don't ask "What's broken?"**

Ask:

> **"At which layer did the communication stop?"**

```text
DNS
 ↓
IP
 ↓
Route
 ↓
Connection
 ↓
Port
 ↓
Security
 ↓
Service
 ↓
Application
```

Find that layer.

Then fix that layer.

That's networking. 🔥

---

# 📚 Navigation

⬅️ Previous: **[17-Network-Troubleshooting.md](17-Network-Troubleshooting.md)**

➡️ Next: **[19-Networking-Mini-Projects.md](19-Networking-Mini-Projects.md)**

🏠 Networking Phase: **[README.md](README.md)**

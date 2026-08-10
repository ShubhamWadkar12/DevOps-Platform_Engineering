# 🚀 Networking Mini Projects

## 🎯 What Are We Building?

We've spent the last few chapters learning:

```text
🌐 Networking Fundamentals
        ↓
🧩 OSI Model
        ↓
📡 TCP/IP
        ↓
🧮 IPv4 & IPv6
        ↓
✂️ Subnetting
        ↓
🛣️ Routing
        ↓
🔄 NAT
        ↓
📨 Protocols
        ↓
🌐 DNS
        ↓
🔥 Firewalls
        ↓
⚖️ Load Balancing
        ↓
☁️ VPC
        ↓
🔗 VPC Peering
        ↓
🔐 VPN
        ↓
🛡️ Network Security
        ↓
🛠️ Troubleshooting
```

Now we're going to combine those concepts into **real-world mini projects**.

The goal isn't to build huge production systems yet.

The goal is:

> **Take networking concepts and turn them into things you can actually build, test, break, and troubleshoot.**

---

# 🗺️ Project Roadmap

| Project | Topic | Difficulty |
|---|---|---|
| 01 | Network Information Tool | 🟢 Easy |
| 02 | DNS Investigation Tool | 🟢 Easy |
| 03 | Port Scanner | 🟡 Medium |
| 04 | Local Web Server | 🟡 Medium |
| 05 | Network Connectivity Monitor | 🟡 Medium |
| 06 | Service Health Checker | 🟡 Medium |
| 07 | Network Troubleshooting Toolkit | 🟡 Medium |
| 08 | TCP Client-Server | 🟠 Advanced |
| 09 | HTTP Reverse Proxy | 🟠 Advanced |
| 10 | Three-Tier Network Design | 🔴 Advanced |
| 11 | AWS VPC Architecture | 🔴 Advanced |
| 12 | Final DevOps Networking Project | 🔴 Advanced |

---

# 🧰 Recommended Environment

Use:

```text
🐧 Ubuntu / WSL
```

Check:

```bash
cat /etc/os-release
```

Useful tools:

```text
ip
ping
dig
nslookup
curl
nc
ss
traceroute
tcpdump
Python
Bash
```

---

# 🚀 Project 01 — Network Information Tool

## 🎯 Objective

Create a script that displays important network information about your Linux machine.

The script should show:

```text
📡 Network Interfaces
🌐 IP Addresses
🛣️ Routing Table
🔎 DNS Configuration
👂 Listening Ports
```

---

# 📁 Project Structure

```text
network-info-tool/
│
├── README.md
└── network-info.sh
```

---

# 🛠️ Create Project

```bash
mkdir -p ~/networking-projects/network-info-tool
cd ~/networking-projects/network-info-tool
```

Create:

```bash
touch network-info.sh
```

---

# 🧑‍💻 Script

```bash
#!/bin/bash

echo "================================="
echo "      NETWORK INFORMATION"
echo "================================="

echo ""
echo "📡 Network Interfaces"
ip link

echo ""
echo "🌐 IP Addresses"
ip addr

echo ""
echo "🛣️ Routing Table"
ip route

echo ""
echo "🔎 DNS Configuration"
cat /etc/resolv.conf

echo ""
echo "👂 Listening Ports"
ss -lntup

echo ""
echo "================================="
echo "        END OF REPORT"
echo "================================="
```

Make executable:

```bash
chmod +x network-info.sh
```

Run:

```bash
./network-info.sh
```

---

# 🧠 What You Learn

```text
Linux Networking
+
Shell Scripting
+
Network Diagnostics
```

This is your first tiny DevOps-style utility.

---

# 🚀 Project 02 — DNS Investigation Tool

## 🎯 Objective

Create a tool that accepts a domain name and displays:

```text
Domain
IPv4 Address
IPv6 Address
DNS Information
```

Example:

```bash
./dns-check.sh google.com
```

---

# 📁 Project Structure

```text
dns-investigator/
│
├── README.md
└── dns-check.sh
```

---

# 🧑‍💻 Script

```bash
#!/bin/bash

DOMAIN=$1

if [ -z "$DOMAIN" ]; then
    echo "Usage: ./dns-check.sh <domain>"
    exit 1
fi

echo "================================="
echo "       DNS INVESTIGATION"
echo "================================="

echo ""
echo "🌐 Domain:"
echo "$DOMAIN"

echo ""
echo "IPv4:"
dig +short A "$DOMAIN"

echo ""
echo "IPv6:"
dig +short AAAA "$DOMAIN"

echo ""
echo "DNS Information:"
dig "$DOMAIN"

echo ""
echo "================================="
```

Make executable:

```bash
chmod +x dns-check.sh
```

Run:

```bash
./dns-check.sh google.com
```

---

# 🎮 Challenge

Test:

```bash
./dns-check.sh github.com
./dns-check.sh amazon.com
./dns-check.sh example.com
```

Compare:

```text
IPv4
IPv6
DNS response
```

---

# 🧠 DevOps Connection

DNS problems are extremely common in:

```text
Microservices
Docker
Kubernetes
AWS
Load Balancers
Service Discovery
```

Understanding DNS now will save you headaches later.

---

# 🚀 Project 03 — TCP Port Scanner

## 🎯 Objective

Build a simple tool that checks whether TCP ports are reachable.

Example:

```bash
./port-scanner.sh localhost
```

Output:

```text
Scanning localhost...

Port 22    → OPEN
Port 80    → CLOSED
Port 443   → OPEN
Port 8080  → OPEN
```

---

# ⚠️ Important

Only scan:

```text
Your own systems
Systems you own
Systems you have explicit permission to test
```

Do not use this project to scan random public systems.

---

# 📁 Project Structure

```text
tcp-port-scanner/
│
├── README.md
└── port-scanner.sh
```

---

# 🧑‍💻 Script

```bash
#!/bin/bash

HOST=$1

if [ -z "$HOST" ]; then
    echo "Usage: ./port-scanner.sh <host>"
    exit 1
fi

echo "================================="
echo "       TCP PORT SCANNER"
echo "================================="

for PORT in 22 53 80 443 3306 5432 6379 8080
do
    if timeout 2 bash -c "</dev/tcp/$HOST/$PORT" 2>/dev/null
    then
        echo "Port $PORT → OPEN"
    else
        echo "Port $PORT → CLOSED/FILTERED"
    fi
done

echo "================================="
```

Make executable:

```bash
chmod +x port-scanner.sh
```

Run against your own machine:

```bash
./port-scanner.sh localhost
```

---

# 🧠 What You Learn

```text
TCP
Ports
Services
Connectivity
Shell Scripting
```

---

# 🚀 Project 04 — Local Web Server

## 🎯 Objective

Build a small HTTP server and understand:

```text
Client
 ↓
TCP
 ↓
HTTP
 ↓
Server
```

---

# 📁 Project Structure

```text
local-web-server/
│
├── README.md
└── index.html
```

Create:

```bash
mkdir -p ~/networking-projects/local-web-server
cd ~/networking-projects/local-web-server
```

Create:

```bash
nano index.html
```

Add:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Networking Lab</title>
</head>
<body>
    <h1>🚀 My Networking Lab</h1>
    <p>This page is being served from Linux.</p>
</body>
</html>
```

---

# ▶️ Start Server

```bash
python3 -m http.server 8080
```

Open another terminal:

```bash
curl http://127.0.0.1:8080
```

---

# 🔎 Inspect

Run:

```bash
ss -lntup | grep 8080
```

Then:

```bash
curl -v http://127.0.0.1:8080
```

---

# 🧠 Architecture

```text
curl
  ↓
127.0.0.1:8080
  ↓
TCP
  ↓
Python HTTP Server
  ↓
index.html
```

---

# 🚀 Project 05 — Network Connectivity Monitor

## 🎯 Objective

Build a script that continuously checks whether a host is reachable.

Example:

```text
🌐 Monitoring google.com

[21:00:01] ✅ Reachable
[21:00:06] ✅ Reachable
[21:00:11] ❌ Unreachable
[21:00:16] ❌ Unreachable
```

---

# 📁 Project Structure

```text
network-monitor/
│
├── README.md
└── monitor.sh
```

---

# 🧑‍💻 Script

```bash
#!/bin/bash

HOST=${1:-8.8.8.8}
INTERVAL=${2:-5}

echo "Monitoring: $HOST"
echo "Interval: ${INTERVAL}s"
echo "Press CTRL+C to stop."

while true
do
    TIMESTAMP=$(date '+%Y-%m-%d %H:%M:%S')

    if ping -c 1 -W 2 "$HOST" > /dev/null 2>&1
    then
        echo "[$TIMESTAMP] ✅ $HOST is reachable"
    else
        echo "[$TIMESTAMP] ❌ $HOST is unreachable"
    fi

    sleep "$INTERVAL"
done
```

Run:

```bash
chmod +x monitor.sh
```

Then:

```bash
./monitor.sh google.com 5
```

Stop:

```text
CTRL + C
```

---

# 🔥 DevOps Connection

This is the basic idea behind:

```text
Monitoring
Health Checks
Availability Checks
Alerting
```

Later you'll use:

```text
Prometheus
Grafana
CloudWatch
Kubernetes Probes
```

---

# 🚀 Project 06 — Service Health Checker

## 🎯 Objective

Check whether an HTTP service is healthy.

Example:

```bash
./health-check.sh https://example.com
```

Expected:

```text
🌐 URL:
https://example.com

HTTP Status:
200

Response Time:
0.18 seconds

Status:
✅ HEALTHY
```

---

# 🧑‍💻 Script

```bash
#!/bin/bash

URL=$1

if [ -z "$URL" ]; then
    echo "Usage: ./health-check.sh <URL>"
    exit 1
fi

echo "================================="
echo "       SERVICE HEALTH CHECK"
echo "================================="

STATUS=$(curl -o /dev/null -s -w "%{http_code}" --max-time 10 "$URL")

TIME=$(curl -o /dev/null -s -w "%{time_total}" --max-time 10 "$URL")

echo ""
echo "URL: $URL"
echo "HTTP Status: $STATUS"
echo "Response Time: ${TIME}s"

if [ "$STATUS" = "200" ]; then
    echo "Status: ✅ HEALTHY"
else
    echo "Status: ❌ UNHEALTHY"
fi

echo "================================="
```

---

# 🎮 Challenge

Test:

```bash
./health-check.sh https://example.com
```

Then test an invalid URL.

Observe:

```text
HTTP status
Response time
Failure behavior
```

---

# 🚀 Project 07 — Network Troubleshooting Toolkit

Now combine the previous projects.

## 🎯 Objective

Create one command that performs:

```text
DNS Check
 ↓
Ping
 ↓
Route
 ↓
Port Test
 ↓
HTTP Test
 ↓
Listening Ports
```

---

# 📁 Project Structure

```text
network-troubleshooting-toolkit/
│
├── README.md
├── network-info.sh
├── dns-check.sh
├── ping-check.sh
├── port-check.sh
├── http-check.sh
└── troubleshoot.sh
```

---

# 🧠 Main Flow

```text
                 TARGET
                   │
          ┌────────┼────────┐
          ↓        ↓        ↓
         DNS      Ping     Route
          │        │        │
          └────────┼────────┘
                   ↓
                 Port
                   ↓
                 HTTP
                   ↓
               Listening
                   ↓
                Summary
```

---

# 🎯 Main Script

Example:

```bash
#!/bin/bash

TARGET=$1

if [ -z "$TARGET" ]; then
    echo "Usage: ./troubleshoot.sh <host>"
    exit 1
fi

echo "================================="
echo "   NETWORK TROUBLESHOOTING"
echo "================================="

echo ""
echo "🌐 DNS"
getent hosts "$TARGET"

echo ""
echo "📡 Connectivity"
ping -c 2 "$TARGET"

echo ""
echo "🛣️ Route"
ip route get "$TARGET" 2>/dev/null

echo ""
echo "👂 Common HTTPS Port"
nc -vz "$TARGET" 443

echo ""
echo "🌍 HTTP/HTTPS"
curl -I --max-time 5 "https://$TARGET"

echo ""
echo "================================="
echo "        CHECK COMPLETE"
echo "================================="
```

---

# 🧠 Important

A real production troubleshooting tool should have:

```text
Better error handling
Timeouts
Logging
Input validation
Structured output
Security considerations
```

This version is intentionally simple for learning.

---

# 🚀 Project 08 — TCP Client-Server

Now we're going to understand networking from the programming side.

## 🎯 Objective

Build:

```text
🖥️ TCP Server
       ↑
       │
       │ TCP
       │
       ↓
💻 TCP Client
```

---

# 📁 Project Structure

```text
tcp-client-server/
│
├── README.md
├── server.py
└── client.py
```

---

# 🧑‍💻 `server.py`

```python
import socket

HOST = "127.0.0.1"
PORT = 5000

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server.bind((HOST, PORT))
server.listen(1)

print(f"🚀 Server listening on {HOST}:{PORT}")

conn, addr = server.accept()

print(f"🔗 Connection from {addr}")

data = conn.recv(1024)

print("📩 Received:", data.decode())

conn.sendall(b"Hello from TCP server!")

conn.close()
server.close()
```

---

# 🧑‍💻 `client.py`

```python
import socket

HOST = "127.0.0.1"
PORT = 5000

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect((HOST, PORT))

client.sendall(b"Hello from TCP client!")

response = client.recv(1024)

print("📩 Server:", response.decode())

client.close()
```

---

# ▶️ Run Server

Terminal 1:

```bash
python3 server.py
```

---

# ▶️ Run Client

Terminal 2:

```bash
python3 client.py
```

---

# 🧠 Architecture

```text
Client
  │
  │ connect()
  ↓
Server
  │
  │ accept()
  ↓
TCP Connection
  │
  ├── send()
  └── recv()
```

---

# 🔥 What You Learn

```text
Sockets
TCP
Client/Server
Ports
Connections
Application Networking
```

This becomes useful later when understanding:

```text
Microservices
Docker
Kubernetes
APIs
Distributed Systems
```

---

# 🚀 Project 09 — HTTP Reverse Proxy

## 🎯 Objective

Understand what a reverse proxy does.

Architecture:

```text
🌍 Client
    ↓
🔀 Reverse Proxy
    ↓
🖥️ Backend Server
```

The client communicates with the proxy instead of directly accessing the backend.

---

# 🏠 Real-Life Analogy

Imagine a hotel.

```text
👤 Guest
   ↓
🧑‍💼 Reception
   ↓
🏨 Correct Room
```

The guest doesn't need to know every internal detail.

The receptionist decides where to send them.

A reverse proxy does something similar:

```text
Client
  ↓
Reverse Proxy
  ↓
Backend
```

---

# 🧪 Simple Python Reverse Proxy Concept

For learning, use an existing reverse proxy such as:

```text
Nginx
```

rather than writing a production proxy from scratch.

Architecture:

```text
🌍 Client
    ↓
    ↓ TCP 80/443
    ↓
🌐 Nginx
    ↓
    ↓ HTTP
    ↓
🐍 Python App
```

---

# 🧪 Local Backend

Start:

```bash
python3 -m http.server 8080
```

Backend:

```text
127.0.0.1:8080
```

Configure Nginx to proxy requests to it.

---

# 🧠 What You Learn

```text
Reverse Proxy
HTTP
Ports
Backend Services
Load Balancing Concepts
```

---

# 🚀 Project 10 — Three-Tier Network Design

Now design something closer to real cloud architecture.

## 🎯 Objective

Create a secure architecture:

```text
🌍 Internet
     ↓
⚖️ Load Balancer
     ↓
🔒 Application
     ↓
🗄️ Database
```

---

# 🏗️ Network Design

Use:

```text
VPC:
10.0.0.0/16
```

Subnets:

```text
Public:
10.0.1.0/24

Private Application:
10.0.2.0/24

Private Database:
10.0.3.0/24
```

---

# 🔐 Security Design

```text
Internet
   ↓
TCP 443
   ↓
Load Balancer
   ↓
Application
   ↓
TCP 5432
   ↓
Database
```

Do NOT design:

```text
Internet
   ↓
Database
```

---

# 🧠 Security Groups

### ALB

```text
Allow:
443

Source:
Internet
```

### Application

```text
Allow:
Application Port

Source:
ALB Security Group
```

### Database

```text
Allow:
5432

Source:
Application Security Group
```

---

# 🎯 Your Task

Create an architecture diagram and explain:

```text
IP Addressing
Subnets
Routing
Security Groups
Ports
Application Flow
Database Flow
```

---

# 🚀 Project 11 — AWS VPC Architecture

Now bring your networking knowledge into AWS.

## 🎯 Objective

Design a VPC:

```text
10.0.0.0/16
```

with:

```text
2 Availability Zones
```

---

# 🏗️ Architecture

```text
                         ☁️ VPC
                     10.0.0.0/16
                           │
             ┌─────────────┴─────────────┐
             ↓                           ↓
           AZ-1                        AZ-2
             │                           │
      ┌──────┴──────┐             ┌──────┴──────┐
      ↓             ↓             ↓             ↓
    Public        Private       Public        Private
    Subnet         App          Subnet         App
      │             │             │             │
     ALB            EC2          ALB            EC2
```

Database:

```text
Private Database Subnets
```

---

# 🧠 Things to Design

Document:

```text
VPC CIDR
Subnet CIDRs
Route Tables
Internet Gateway
NAT Gateway
Security Groups
NACLs
Load Balancer
Application
Database
```

---

# ⚠️ Cost Awareness

AWS resources can cost money.

Before creating infrastructure:

```text
Check pricing
Check free-tier eligibility
Use the smallest appropriate resources
Delete resources after the lab
```

For learning, you can also complete this project as:

```text
Architecture Diagram
+
Terraform Configuration
```

without actually keeping expensive resources running.

---

# 🚀 Project 12 — Final DevOps Networking Project

## 🏆 Build a Production-Style Network Architecture

This is your final networking project.

Design:

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
                         ⚖️ Load Balancer
                              │
                 ┌────────────┴────────────┐
                 ↓                         ↓
              AZ-1                      AZ-2
                 │                         │
          🔒 App Server              🔒 App Server
                 │                         │
                 └────────────┬────────────┘
                              ↓
                        🔒 Private DB
                              │
                              ↓
                           🗄️ RDS
```

---

# 🏢 Add Hybrid Connectivity

Now add:

```text
🏢 On-Premises
       │
       🔐 VPN
       │
       ↓
☁️ AWS
```

---

# 🔗 Add VPC Connectivity

Add:

```text
☁️ Production VPC
       │
       🔗
       │
☁️ Shared Services VPC
```

---

# 🚦 Think About Scaling

If you eventually have:

```text
Dev VPC
Test VPC
Production VPC
Security VPC
Logging VPC
Shared Services VPC
```

ask:

> Would individual VPC Peering connections still be the best design?

Investigate:

```text
Transit Gateway
```

---

# 🧠 Final Architecture

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
                            ⚖️ Load Balancer
                                  │
                     ┌────────────┴────────────┐
                     ↓                         ↓
                  AZ-1                      AZ-2
                     │                         │
                  App-1                     App-2
                     │                         │
                     └────────────┬────────────┘
                                  ↓
                           Private Database
                                  │
                                  ↓
                               🗄️ RDS


                 🏢 On-Premises
                        │
                        🔐 VPN
                        │
                        ↓
                    ☁️ AWS VPC


             ☁️ Shared Services VPC
                        │
                        🔗
                        │
                 Production VPC
```

---

# 🧠 Final Project Requirements

Your architecture should demonstrate:

## Networking

- [ ] IPv4 addressing
- [ ] CIDR planning
- [ ] Subnetting
- [ ] Routing
- [ ] NAT
- [ ] DNS
- [ ] Load Balancing

## AWS

- [ ] VPC
- [ ] Public Subnets
- [ ] Private Subnets
- [ ] Route Tables
- [ ] Internet Gateway
- [ ] NAT Gateway
- [ ] Security Groups
- [ ] NACLs
- [ ] VPC Peering
- [ ] VPN
- [ ] Transit Gateway concept

## Security

- [ ] Least Privilege
- [ ] Network Segmentation
- [ ] Private Database
- [ ] Encryption
- [ ] Firewall
- [ ] WAF
- [ ] Monitoring
- [ ] Logging

## Troubleshooting

- [ ] DNS
- [ ] Routing
- [ ] Ports
- [ ] Connectivity
- [ ] Security Groups
- [ ] NACLs
- [ ] Application
- [ ] Logs
- [ ] Packet Capture

---

# 🧪 Final Troubleshooting Scenario

Your application suddenly reports:

```text
❌ Database connection timeout
```

Architecture:

```text
Application
     │
     ↓
Security Group
     │
     ↓
Private Network
     │
     ↓
Database
```

Don't immediately change the Security Group.

Use:

```text
1. Resolve database hostname
        ↓
2. Check destination IP
        ↓
3. Check route
        ↓
4. Test TCP 5432
        ↓
5. Check Security Group
        ↓
6. Check NACL
        ↓
7. Check OS firewall
        ↓
8. Check database listener
        ↓
9. Check database logs
        ↓
10. Verify application configuration
```

---

# 📝 Project Documentation

For every project, create a `README.md` containing:

```text
# Project Name

## 🎯 Objective

## 🏗️ Architecture

## 🛠️ Technologies

## 📋 Requirements

## 🚀 Setup

## ▶️ Usage

## 🧪 Testing

## 🔎 Troubleshooting

## 🧠 What I Learned

## 📸 Screenshots

## 🚀 Future Improvements
```

---

# 📸 Document Your Work

For your GitHub portfolio, capture:

```text
Terminal Output
Architecture Diagram
Network Commands
Test Results
Troubleshooting Results
```

Example:

```text
screenshots/
├── network-info.png
├── dns-test.png
├── port-test.png
├── tcpdump.png
└── aws-vpc.png
```

---

# 💼 What Makes These Projects Good for DevOps?

You're not just learning:

```text
"How does DNS work?"
```

You're building:

```text
DNS Investigation Tool
```

You're not just learning:

```text
"What is a port?"
```

You're building:

```text
Port Testing Tool
```

You're not just learning:

```text
"What is monitoring?"
```

You're building:

```text
Network Monitor
```

You're not just learning:

```text
"What is troubleshooting?"
```

You're building:

```text
Troubleshooting Toolkit
```

This is how theory becomes practical engineering.

---

# 🔥 Skills You're Building

```text
Linux
   +
Networking
   +
Bash
   +
Python
   +
Troubleshooting
   +
Cloud Networking
   +
Security
   +
Automation
```

That's a very useful foundation for:

```text
☁️ DevOps
🏗️ Platform Engineering
🔐 DevSecOps
☸️ Kubernetes
🐳 Docker
🚀 CI/CD
```

---

# 🏆 Final Networking Project Checklist

Before leaving the Networking section, you should be able to:

- [ ] Build a network information script
- [ ] Investigate DNS
- [ ] Test TCP ports
- [ ] Run a local HTTP server
- [ ] Monitor network connectivity
- [ ] Check service health
- [ ] Build a troubleshooting toolkit
- [ ] Create a TCP client/server
- [ ] Understand reverse proxies
- [ ] Design a three-tier network
- [ ] Design an AWS VPC
- [ ] Design public/private subnets
- [ ] Design Security Groups
- [ ] Explain VPC Peering
- [ ] Explain VPN
- [ ] Explain Transit Gateway
- [ ] Troubleshoot network failures
- [ ] Capture packets with `tcpdump`
- [ ] Document networking projects on GitHub

---

# 🧠 Final Takeaway

Networking isn't about memorizing:

```text
22
53
80
443
3306
5432
```

It's about understanding the flow:

```text
👤 Client
   ↓
🌐 DNS
   ↓
📍 IP
   ↓
🛣️ Route
   ↓
🔌 Port
   ↓
🔥 Firewall
   ↓
🛡️ Security
   ↓
🖥️ Service
   ↓
📦 Application
```

When something breaks:

> **Find where the flow stopped.**

That's the networking skill you want to carry into every future DevOps project. 🔥

---

# 📚 Navigation

⬅️ Previous: **[18-Networking-Hands-on-Labs.md](18-Networking-Hands-on-Labs.md)**

➡️ Next: **[20-Networking-Checklist.md](20-Networking-Checklist.md)**

🏠 Networking Phase: **[README.md](README.md)**

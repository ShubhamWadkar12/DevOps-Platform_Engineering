# 🛠️ Network Troubleshooting

## 🎯 What Are We Learning?

So far, we've learned how networks are built:

```text
IP Addressing
      ↓
Subnetting
      ↓
Routing
      ↓
NAT
      ↓
Protocols
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
      ↓
Network Security
```

Now comes the part that every DevOps Engineer eventually learns the hard way:

> **"It worked yesterday. Why is it broken today?"** 😂

This chapter is about finding the answer systematically.

---

# 🧠 What Is Network Troubleshooting?

Network troubleshooting is the process of:

```text
Identifying
    ↓
Analyzing
    ↓
Testing
    ↓
Isolating
    ↓
Fixing
    ↓
Verifying
```

a network problem.

The goal is not to randomly run commands.

The goal is:

> **Find exactly where communication is failing.**

---

# 🏠 Real-Life Example

Imagine you order food:

```text
🍕 You
 ↓
📱 App
 ↓
🌐 Internet
 ↓
🏪 Restaurant
 ↓
🛵 Delivery Partner
 ↓
🏠 Your House
```

Your food doesn't arrive.

Possible problems:

```text
📱 App broken
🌐 Internet broken
🏪 Restaurant closed
🛵 Delivery unavailable
🏠 Wrong address
```

You wouldn't blame the delivery driver immediately.

You would check each stage.

Network troubleshooting works the same way.

---

# 🌐 Network Troubleshooting Mental Model

When:

```text
Client ❌ Server
```

don't immediately say:

> "The network is down."

Break the path into layers:

```text
1️⃣ DNS
   ↓
2️⃣ IP Address
   ↓
3️⃣ Routing
   ↓
4️⃣ Connectivity
   ↓
5️⃣ Port
   ↓
6️⃣ Firewall
   ↓
7️⃣ Application
```

---

# 🔥 The Golden Troubleshooting Flow

Use this mental model:

```text
                    ❓ Problem
                       │
                       ↓
                  DNS Working?
                       │
                ┌──────┴──────┐
                │             │
               NO            YES
                │             │
                ↓             ↓
            Fix DNS       Correct IP?
                              │
                       ┌──────┴──────┐
                       │             │
                      NO            YES
                       │             │
                       ↓             ↓
                  Fix DNS/IP      Route?
                                    │
                              ┌─────┴─────┐
                              │           │
                             NO          YES
                              │           │
                              ↓           ↓
                        Fix Routing   Port Open?
                                          │
                                    ┌─────┴─────┐
                                    │           │
                                   NO          YES
                                    │           │
                                    ↓           ↓
                               Firewall?   Application?
```

This is much better than:

```text
❌ Restart everything
❌ Delete server
❌ Recreate VPC
❌ Blame AWS
```

😂

---

# 🧠 Step 1 — Understand the Problem

Before running commands, ask:

```text
What exactly is failing?
```

Bad:

```text
"The network isn't working."
```

Good:

```text
"Application server 10.0.2.10
cannot connect to PostgreSQL
10.0.3.10 on TCP 5432."
```

Now you have something testable.

---

# 🎯 Define the Problem

Collect:

```text
Source
Destination
Protocol
Port
Time
Error Message
Expected Behavior
Actual Behavior
```

Example:

```text
Source:
10.0.2.10

Destination:
10.0.3.10

Protocol:
TCP

Port:
5432

Expected:
Database connection

Actual:
Connection timeout
```

Now troubleshooting becomes much easier.

---

# 🔎 Step 2 — Check DNS

Suppose your application uses:

```text
database.internal
```

First ask:

> Does the name resolve?

Use:

```bash
dig database.internal
```

or:

```bash
nslookup database.internal
```

---

# 🧪 Example

Run:

```bash
dig example.com
```

Look for:

```text
ANSWER SECTION
```

You might see:

```text
example.com.    A    93.184.216.34
```

This tells you:

```text
example.com
     ↓
93.184.216.34
```

---

# 🚨 DNS Failure

Suppose:

```bash
dig database.internal
```

returns:

```text
NXDOMAIN
```

Then the problem may be:

```text
DNS Record
DNS Server
DNS Zone
DNS Configuration
```

Don't waste time checking the database firewall yet.

If the hostname can't resolve, you haven't even reached the database.

---

# 🧠 DNS Troubleshooting

Ask:

```text
1. What hostname is being used?

2. Does it resolve?

3. Which DNS server is being used?

4. Is the DNS record correct?

5. Is the client allowed to query that DNS server?

6. Is this an internal/private DNS name?
```

---

# 🛠️ Useful Commands

```bash
dig example.com
```

```bash
nslookup example.com
```

```bash
getent hosts example.com
```

```bash
cat /etc/resolv.conf
```

---

# 🔎 Step 3 — Check IP Address

Once DNS resolves:

```text
database.internal
      ↓
10.0.3.10
```

verify that the IP is actually the expected destination.

Use:

```bash
getent hosts database.internal
```

or:

```bash
dig +short database.internal
```

---

# 🧠 Common Problem

Your application expects:

```text
10.0.3.10
```

but DNS returns:

```text
10.0.8.10
```

Now your application might be connecting to the wrong system.

So:

```text
DNS working
≠
DNS configuration correct
```

---

# 🔎 Step 4 — Check Routing

Now ask:

> "Does my machine know where to send traffic?"

Use:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
10.0.0.0/16 via 192.168.1.254 dev eth0
```

---

# 🛣️ Real-Life Analogy

Imagine you know the destination:

```text
🏢 Office
```

But your GPS says:

```text
❌ No route available
```

You know where you're going.

But you don't know how to get there.

That's a routing problem.

---

# 🧪 Test a Specific Route

Use:

```bash
ip route get 10.0.3.10
```

This can show which route/interface the system would use for that destination.

Example:

```text
10.0.3.10 via 192.168.1.254 dev eth0
```

Now you know:

```text
Destination:
10.0.3.10

Gateway:
192.168.1.254

Interface:
eth0
```

---

# 🔎 Step 5 — Test Basic Connectivity

A common first test:

```bash
ping <IP>
```

Example:

```bash
ping 10.0.3.10
```

---

# ⚠️ Important: Ping Is Not Proof

If ping succeeds:

```text
ICMP works ✅
```

But that doesn't mean:

```text
TCP 5432 works
HTTPS works
Application works
```

Likewise, if ping fails:

```text
It does NOT automatically prove the host is unreachable.
```

ICMP may simply be blocked.

---

# 🧠 Better Question

Don't ask:

> "Can I ping the server?"

Ask:

> "Can I reach the service I actually need?"

For HTTPS:

```bash
curl -v https://example.com
```

For TCP:

```bash
nc -vz <IP> <PORT>
```

---

# 🔎 Step 6 — Check the Port

Suppose:

```text
Database:
10.0.3.10

PostgreSQL:
5432
```

Test:

```bash
nc -vz 10.0.3.10 5432
```

---

# 🧪 Possible Results

### Success

```text
Connection succeeded
```

Then:

```text
Network path
+
Port
```

are likely working.

The problem may be:

```text
Authentication
Application
Database Configuration
```

---

### Connection Refused

Example:

```text
Connection refused
```

This often means the destination is reachable but nothing is accepting the connection on that port, or an active device is rejecting it.

Investigate:

```text
Is the service running?
Is it listening?
Is it bound to the correct interface?
```

---

### Timeout

Example:

```text
Connection timed out
```

Possible causes:

```text
Routing
Firewall
Security Group
NACL
Network ACL
Network path
Service filtering
```

A timeout does not identify one specific cause by itself.

---

# 🧠 Connection Refused vs Timeout

| Error | Common Direction |
|---|---|
| Connection refused | Host reachable, service not accepting / explicit rejection |
| Timeout | Traffic may be filtered, dropped, or path may be broken |
| DNS failure | Name resolution problem |
| No route | Routing problem |

These are clues, not absolute diagnoses.

---

# 🔎 Step 7 — Check Listening Services

On the destination server:

```bash
ss -lntup
```

Look for:

```text
LISTEN
```

Example:

```text
LISTEN 0 128 0.0.0.0:8080
```

This means a process is listening on:

```text
TCP 8080
```

---

# 🧠 Important Difference

Suppose the application is listening on:

```text
127.0.0.1:8080
```

Then:

```text
Local machine → ✅
Remote machine → ❌
```

because the application is only bound to the loopback interface.

---

# 🧪 Example

Run:

```bash
ss -lntp
```

You might see:

```text
127.0.0.1:8080
```

instead of:

```text
0.0.0.0:8080
```

This can explain why a service works locally but not remotely.

---

# 🔎 Step 8 — Check Firewall

Now investigate:

```text
🔥 Host Firewall
🛡️ Security Group
🧱 NACL
🔥 Network Firewall
```

Linux examples:

```bash
sudo ufw status
```

or:

```bash
sudo nft list ruleset
```

or, on systems where legacy iptables is in use:

```bash
sudo iptables -L
```

---

# ⚠️ Don't Blindly Change Firewall Rules

Especially on:

```text
Production
Remote Servers
Cloud Servers
SSH Sessions
```

A careless firewall command can lock you out.

Better approach:

```text
Inspect
 ↓
Understand
 ↓
Change
 ↓
Verify
```

---

# ☁️ AWS Troubleshooting

For AWS, investigate:

```text
VPC
 ↓
Subnet
 ↓
Route Table
 ↓
Internet/NAT Gateway
 ↓
Security Group
 ↓
NACL
 ↓
Instance
 ↓
Application
```

---

# 🔎 AWS Security Group Check

Suppose:

```text
Application
10.0.2.10

Database
10.0.3.10
```

Database uses:

```text
TCP 5432
```

Check whether the database Security Group allows:

```text
TCP 5432
Source:
Application Security Group
```

---

# 🔎 AWS Route Table Check

Suppose:

```text
Application:
10.0.2.0/24

Database:
10.0.3.0/24
```

Check whether the route configuration allows traffic between the subnets.

Within the same VPC, the VPC's local route normally provides connectivity between its CIDR ranges, subject to security controls.

---

# 🔎 VPC Peering Troubleshooting

Suppose:

```text
VPC A
10.0.0.0/16

      🔗

VPC B
10.1.0.0/16
```

Check:

```text
1. CIDRs don't overlap
2. Peering is active
3. VPC A route → 10.1.0.0/16
4. VPC B route → 10.0.0.0/16
5. Security Groups
6. NACLs
7. Destination service
8. DNS if hostname is used
```

---

# 🔎 VPN Troubleshooting

Suppose:

```text
🏢 Office
     │
     🔐 VPN
     │
     ↓
☁️ AWS
```

VPN says:

```text
CONNECTED ✅
```

but application access fails.

Don't stop there.

Check:

```text
VPN Tunnel
     ↓
Routes
     ↓
Security
     ↓
DNS
     ↓
Port
     ↓
Application
```

---

# 🔎 Load Balancer Troubleshooting

Suppose:

```text
🌍 User
   ↓
⚖️ Load Balancer
   ↓
🖥️ Application
```

User receives:

```text
502 Bad Gateway
```

Possible areas:

```text
Load Balancer
 ↓
Target Health
 ↓
Security Group
 ↓
Target Port
 ↓
Application
```

---

# ❤️ Health Checks

Check whether backend targets are:

```text
Healthy
```

or:

```text
Unhealthy
```

Suppose:

```text
ALB
 │
 ├── Server 1 → ✅
 ├── Server 2 → ❌
 └── Server 3 → ❌
```

Investigate:

```text
Health Check Path
Health Check Port
Application Status
Security Group
Network Connectivity
```

---

# 🔎 Step 9 — Check Application Logs

If networking appears healthy:

```text
DNS ✅
Route ✅
Port ✅
Firewall ✅
```

look at the application.

Example:

```bash
journalctl -u nginx
```

or:

```bash
journalctl -u <service>
```

For Docker:

```bash
docker logs <container>
```

For Kubernetes:

```bash
kubectl logs <pod>
```

---

# 🧠 The Application May Be the Problem

Sometimes:

```text
Network → ✅
```

but:

```text
Application → ❌
```

Examples:

```text
Wrong database password
Application crashed
Wrong environment variable
Wrong port
Wrong bind address
Certificate problem
Application dependency unavailable
```

---

# 🧪 Step 10 — Test Locally

Suppose the application runs on:

```text
localhost:8080
```

Run on the server:

```bash
curl http://127.0.0.1:8080
```

If this works:

```text
Application is probably running locally.
```

Now test using the server's private IP:

```bash
curl http://10.0.2.10:8080
```

If:

```text
localhost → ✅
private IP → ❌
```

investigate:

```text
Bind Address
Firewall
Network Interface
```

---

# 🧠 Super Useful Pattern

## Case 1

```text
localhost → ❌
private IP → ❌
remote → ❌
```

Likely:

```text
Application/service problem
```

---

## Case 2

```text
localhost → ✅
private IP → ❌
remote → ❌
```

Likely:

```text
Bind Address
Firewall
Network Interface
```

---

## Case 3

```text
localhost → ✅
private IP → ✅
remote → ❌
```

Likely:

```text
Network path
Security Group
NACL
Firewall
Routing
```

This isn't absolute, but it's a useful troubleshooting clue.

---

# 🔎 Step 11 — Trace the Network Path

Use:

```bash
traceroute example.com
```

or:

```bash
tracepath example.com
```

Depending on your Linux environment.

For TCP-based testing, tools such as:

```bash
traceroute -T
```

may be useful where supported.

---

# 🧠 What Does Traceroute Show?

It attempts to show the path packets take toward a destination.

Conceptually:

```text
Your Machine
    ↓
Router 1
    ↓
Router 2
    ↓
Router 3
    ↓
Destination
```

If the path stops at:

```text
Router 2
```

that gives you a clue about where to investigate.

---

# ⚠️ Traceroute Is Not Perfect

Some networks:

```text
Block ICMP
Rate-limit responses
Hide routers
Filter probes
```

So:

```text
Traceroute failure
≠
Application failure
```

Treat it as evidence, not absolute truth.

---

# 🔎 Step 12 — Packet Capture

When basic troubleshooting isn't enough:

> **Capture packets.**

A common Linux tool:

```bash
tcpdump
```

Example:

```bash
sudo tcpdump -i any port 443
```

This can help you determine whether traffic is:

```text
Leaving the source
Arriving at destination
Returning
Being retransmitted
```

---

# 🧠 Packet Capture Mental Model

Suppose:

```text
Client
  ↓
Server
```

You can ask:

```text
Did SYN leave?
      ↓
Did SYN arrive?
      ↓
Did SYN-ACK return?
      ↓
Did ACK complete?
```

This helps troubleshoot TCP connectivity.

---

# 🤝 TCP Three-Way Handshake

A simplified TCP connection:

```text
Client                    Server

  SYN  ─────────────────→
       ←──────────────── SYN-ACK
  ACK  ─────────────────→

        Connection Established
```

---

# 🚨 If SYN Leaves But No SYN-ACK Returns

Possible causes include:

```text
Firewall
Routing
Destination unavailable
Security Group
NACL
Packet filtering
```

Again:

> It's a clue, not a single guaranteed diagnosis.

---

# 🧠 TCP Troubleshooting

Think:

```text
SYN
 ↓
Did it leave?

SYN-ACK
 ↓
Did it return?

ACK
 ↓
Did connection establish?
```

---

# 🛠️ Useful Linux Commands

## Interface Information

```bash
ip addr
```

---

## Routing

```bash
ip route
```

---

## Specific Route

```bash
ip route get <IP>
```

---

## DNS

```bash
dig <hostname>
```

```bash
nslookup <hostname>
```

---

## Connectivity

```bash
ping <IP>
```

---

## Trace Route

```bash
traceroute <host>
```

---

## TCP Port Test

```bash
nc -vz <IP> <PORT>
```

---

## HTTP Test

```bash
curl -v http://<IP>:<PORT>
```

---

## HTTPS Test

```bash
curl -vk https://<hostname>
```

Use `-k` only when you intentionally want to ignore certificate verification for testing.

---

## Listening Ports

```bash
ss -lntup
```

---

## Processes

```bash
ps aux
```

---

## Service Status

```bash
systemctl status <service>
```

---

## Service Logs

```bash
journalctl -u <service>
```

---

## Packet Capture

```bash
sudo tcpdump -i any
```

---

# 🧰 Troubleshooting Toolkit

Your basic toolkit:

```text
ip
ping
dig
nslookup
getent
traceroute
tracepath
nc
curl
ss
tcpdump
systemctl
journalctl
```

Don't memorize commands blindly.

Understand what question each command answers.

---

# 🧠 Command → Question

| Command | Question |
|---|---|
| `ip addr` | What IP/interface do I have? |
| `ip route` | Where does traffic go? |
| `ip route get` | Which route will this destination use? |
| `ping` | Does ICMP reach the destination? |
| `dig` | Does DNS resolve? |
| `nslookup` | Does DNS resolve? |
| `getent hosts` | Can the system resolve this name? |
| `traceroute` | What path is being observed? |
| `nc` | Can I connect to this TCP/UDP port? |
| `curl` | Does the application/HTTP service respond? |
| `ss` | What ports are listening? |
| `tcpdump` | What packets are actually visible? |
| `systemctl` | Is the service running? |
| `journalctl` | What does the service/system log say? |

---

# 🚨 Common Network Errors

## `Temporary failure in name resolution`

Likely area:

```text
DNS
```

Check:

```bash
cat /etc/resolv.conf
dig example.com
```

---

# 🚨 `No route to host`

Likely area:

```text
Routing
Network configuration
Firewall
```

Check:

```bash
ip route
ip route get <IP>
```

---

# 🚨 `Connection refused`

Likely areas:

```text
Service not listening
Wrong port
Application configuration
Firewall rejection
```

Check:

```bash
ss -lntup
```

---

# 🚨 `Connection timed out`

Possible areas:

```text
Routing
Firewall
Security Group
NACL
Network path
Destination unavailable
```

---

# 🚨 `Host is unreachable`

Possible areas:

```text
Routing
Interface
Gateway
Network configuration
```

---

# 🚨 `502 Bad Gateway`

Often investigate:

```text
Load Balancer
Backend Health
Backend Port
Application
```

---

# 🚨 `503 Service Unavailable`

Could indicate:

```text
No healthy backend
Application unavailable
Service overloaded
Load Balancer configuration
```

The exact cause depends on the architecture.

---

# 🚨 `504 Gateway Timeout`

Often investigate:

```text
Backend response time
Routing
Firewall
Application
Database dependency
Load Balancer timeout
```

---

# 🧠 Troubleshooting Decision Tree

Use this whenever an application cannot connect.

```text
                    Application Failing
                           │
                           ↓
                    Does DNS resolve?
                       /          \
                     NO            YES
                     ↓              ↓
                 Fix DNS        Correct IP?
                                   /    \
                                 NO      YES
                                 ↓        ↓
                             Fix DNS    Route?
                                          /  \
                                        NO    YES
                                        ↓      ↓
                                   Fix Route  Port?
                                               / \
                                             NO   YES
                                             ↓     ↓
                                        Firewall? App?
```

---

# 🎯 Example: Website Is Down

User reports:

> "The website isn't opening."

Don't start changing things randomly.

---

## Step 1 — DNS

```bash
dig example.com
```

If:

```text
No answer
```

investigate DNS.

---

## Step 2 — Test HTTPS

```bash
curl -v https://example.com
```

---

## Step 3 — Check Route

```bash
ip route
```

---

## Step 4 — Check Port

```bash
nc -vz example.com 443
```

---

## Step 5 — Check Load Balancer

Check:

```text
Listener
Target Group
Target Health
Security Group
```

---

## Step 6 — Check Application

On backend:

```bash
systemctl status nginx
```

or:

```bash
systemctl status <application>
```

---

## Step 7 — Check Logs

```bash
journalctl -u nginx
```

or application logs.

---

# 🎯 Example: Database Connection Failure

Application:

```text
10.0.2.10
```

Database:

```text
10.0.3.10
```

Port:

```text
5432
```

Application says:

```text
Connection timed out
```

Troubleshoot:

```text
1. DNS
   ↓
2. Route
   ↓
3. Security Group
   ↓
4. NACL
   ↓
5. Database listening
   ↓
6. Firewall
   ↓
7. Credentials
   ↓
8. Database logs
```

---

# 🧠 Notice Something Important

Networking isn't always the problem.

You can have:

```text
Network ✅
```

but:

```text
Authentication ❌
```

For example:

```text
TCP 5432
   ↓
Connection succeeds
   ↓
PostgreSQL
   ↓
Wrong password
   ↓
❌ Login failed
```

So distinguish:

```text
Connectivity
```

from:

```text
Application Authentication
```

---

# 🏗️ DevOps Troubleshooting Workflow

In production, think:

```text
                 🚨 Incident
                     │
                     ↓
                 Observe
                     │
                     ↓
               Define Scope
                     │
                     ↓
              Collect Evidence
                     │
                     ↓
              Form Hypothesis
                     │
                     ↓
                  Test
                     │
                     ↓
               Find Root Cause
                     │
                     ↓
                  Fix
                     │
                     ↓
                Verify
                     │
                     ↓
               Document
```

---

# 🧠 Don't Guess — Test

Bad troubleshooting:

```text
"It might be DNS."

Change DNS.

Still broken.

"It might be firewall."

Change firewall.

Still broken.

"It might be AWS."

😭
```

Good troubleshooting:

```text
Hypothesis:
DNS is broken.

Test:
dig database.internal

Result:
IP returned.

Conclusion:
DNS probably isn't the immediate problem.

Next hypothesis:
Routing.
```

This is how good engineers troubleshoot.

---

# 🔥 Evidence-Based Troubleshooting

Always collect:

```text
Logs
Metrics
Commands
Packet captures
Error messages
Configuration
Routes
Security rules
```

Then form a hypothesis.

---

# 🧪 Hands-on Lab 1 — Your Linux Machine

Run:

```bash
ip addr
```

Record:

```text
Interface:
IPv4:
```

Then:

```bash
ip route
```

Record:

```text
Default Gateway:
Interface:
```

---

# 🧪 Hands-on Lab 2 — DNS

Run:

```bash
dig google.com
```

Find:

```text
DNS Server
Resolved IP
Response Status
```

Then:

```bash
getent hosts google.com
```

Compare the results.

---

# 🧪 Hands-on Lab 3 — Connectivity

Run:

```bash
ping -c 4 8.8.8.8
```

Then:

```bash
ping -c 4 google.com
```

Compare.

If the first works but the second doesn't:

```text
IP connectivity works
DNS may be the problem
```

This is a useful troubleshooting experiment.

---

# 🧪 Hands-on Lab 4 — HTTPS

Run:

```bash
curl -I https://example.com
```

Check:

```text
HTTP Status
Headers
```

---

# 🧪 Hands-on Lab 5 — Port

Run:

```bash
nc -vz example.com 443
```

You are testing:

```text
TCP
Port 443
```

---

# 🧪 Hands-on Lab 6 — Listening Services

Run:

```bash
ss -lntup
```

Find at least:

```text
One listening TCP port
```

Document:

```text
Port:
Process:
Address:
```

---

# 🧪 Hands-on Lab 7 — Local Web Server

Start a simple web server:

```bash
mkdir -p ~/network-lab
cd ~/network-lab
echo "Network Troubleshooting Lab" > index.html
python3 -m http.server 8080
```

In another terminal:

```bash
curl http://127.0.0.1:8080
```

Expected:

```text
Network Troubleshooting Lab
```

Now inspect:

```bash
ss -lntup
```

You should see the server listening on port:

```text
8080
```

---

# 🧪 Hands-on Lab 8 — Test Your Own Service

Run:

```bash
nc -vz 127.0.0.1 8080
```

You should get a successful connection.

Now your troubleshooting flow is:

```text
Service
 ↓
Listening Port
 ↓
TCP Connection
 ↓
HTTP Response
```

---

# 🎮 Troubleshooting Challenge 1

You run:

```bash
curl https://example.com
```

and get:

```text
Could not resolve host
```

What do you check first?

### Answer:

```text
DNS
```

---

# 🎮 Troubleshooting Challenge 2

You run:

```bash
nc -vz 10.0.2.10 8080
```

and get:

```text
Connection refused
```

What should you investigate?

### Answer:

```text
Is something listening on port 8080?
```

Use:

```bash
ss -lntup
```

---

# 🎮 Troubleshooting Challenge 3

You get:

```text
Connection timed out
```

What areas could cause this?

### Answer:

```text
Routing
Firewall
Security Group
NACL
Network path
Destination availability
```

---

# 🎮 Troubleshooting Challenge 4

You run:

```bash
ping 10.0.2.10
```

and it fails.

Can you conclude:

> "The server is down"?

### Answer:

```text
No ❌
```

ICMP could be blocked.

Test the actual application port.

---

# 🎮 Troubleshooting Challenge 5

Your application works with:

```bash
curl http://127.0.0.1:8080
```

but fails from another machine.

What should you investigate?

### Answer:

```text
Bind address
Firewall
Security Group
NACL
Routing
```

---

# 🎮 Troubleshooting Challenge 6

Your VPN says:

```text
CONNECTED ✅
```

but:

```text
10.0.3.10
```

is unreachable.

What do you check?

### Answer:

```text
Route
VPN configuration
Security Group
NACL
Firewall
Return route
Destination service
```

---

# 🎮 Troubleshooting Challenge 7

Your load balancer returns:

```text
502
```

What should you inspect?

### Answer:

```text
Backend health
Backend port
Security Group
Application
Application logs
```

---

# 🧠 Network Troubleshooting Cheat Sheet

```text
🌐 DNS
→ dig
→ nslookup
→ getent

🛣️ Routing
→ ip route
→ ip route get

📡 Connectivity
→ ping

🚦 Port
→ nc

🌍 HTTP/HTTPS
→ curl

👂 Listening Services
→ ss

🧭 Path
→ traceroute
→ tracepath

📦 Packets
→ tcpdump

⚙️ Service
→ systemctl

📜 Logs
→ journalctl
```

---

# 🧠 Golden Rules

```text
1. Define the exact problem.

2. Know the source.

3. Know the destination.

4. Check DNS.

5. Check IP.

6. Check routing.

7. Check connectivity.

8. Check the actual port.

9. Check firewalls/security controls.

10. Check the application.

11. Check logs.

12. Verify the fix.
```

---

# 💼 Interview Corner

### Q: How do you troubleshoot a network connectivity issue?

> I first define the source, destination, protocol, port, and error. Then I check DNS, IP addressing, routing, connectivity, the target port, firewalls/security controls, and finally the application and logs.

---

### Q: What is the difference between `ping` and `curl`?

```text
ping
→ Tests ICMP reachability

curl
→ Tests application-level protocols such as HTTP/HTTPS
```

---

### Q: What does `ip route` show?

> It displays the system's routing table.

---

### Q: What does `ip route get <IP>` do?

> It shows the route the system would use to reach a particular destination.

---

### Q: What does `ss -lntup` show?

> It shows listening network sockets and associated processes when permissions allow.

---

### Q: What is the difference between connection refused and timeout?

```text
Connection refused
→ Destination was reached but connection wasn't accepted/rejected.

Timeout
→ Traffic didn't receive the expected response within the timeout.
```

Possible causes depend on the environment.

---

### Q: Does ping prove that an application is working?

```text
No ❌
```

Ping tests ICMP, not the application's actual protocol.

---

### Q: What is `tcpdump` used for?

> `tcpdump` captures and displays network packets so you can inspect traffic at the packet level.

---

### Q: What would you check if DNS works but an application is unreachable?

```text
IP
 ↓
Route
 ↓
Port
 ↓
Firewall
 ↓
Security Group
 ↓
NACL
 ↓
Application
```

---

### Q: What would you check if localhost works but remote access fails?

> I would check the application's bind address, host firewall, cloud security controls, routing, and network access rules.

---

### Q: What would you check if an AWS EC2 instance cannot reach another EC2?

```text
VPC CIDR
 ↓
Route Table
 ↓
Security Group
 ↓
NACL
 ↓
OS Firewall
 ↓
Service Port
 ↓
Application
```

---

### Q: How would you troubleshoot a 504 from a load balancer?

> I would check target health, backend connectivity, backend port, security controls, application response time, and application logs.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain network troubleshooting
- [ ] Define a network problem precisely
- [ ] Identify source and destination
- [ ] Check DNS
- [ ] Check IP addressing
- [ ] Check routing
- [ ] Use `ip route`
- [ ] Use `ip route get`
- [ ] Understand `ping`
- [ ] Understand why ping isn't enough
- [ ] Test TCP ports with `nc`
- [ ] Test HTTP/HTTPS with `curl`
- [ ] Check listening ports with `ss`
- [ ] Check services with `systemctl`
- [ ] Check logs with `journalctl`
- [ ] Use `traceroute`
- [ ] Understand traceroute limitations
- [ ] Understand TCP connection establishment
- [ ] Use `tcpdump`
- [ ] Troubleshoot DNS failures
- [ ] Troubleshoot routing failures
- [ ] Troubleshoot port failures
- [ ] Troubleshoot firewall problems
- [ ] Troubleshoot AWS Security Groups
- [ ] Troubleshoot NACLs
- [ ] Troubleshoot VPC Peering
- [ ] Troubleshoot VPN connectivity
- [ ] Troubleshoot Load Balancers
- [ ] Distinguish network problems from application problems
- [ ] Use evidence-based troubleshooting
- [ ] Follow a systematic troubleshooting workflow

---

# 🎯 Mini Project

## 🚨 Production Incident: Website Down

Imagine you are the DevOps Engineer on call.

At:

```text
02:15 AM
```

you receive:

```text
🚨 ALERT

Production website is unavailable.
```

Architecture:

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
                   ┌──────────┴──────────┐
                   ↓                     ↓
                EC2-A                 EC2-B
                   │                     │
                   └──────────┬──────────┘
                              ↓
                           🗄️ RDS
```

---

# 🔍 Incident Information

Users report:

```text
Website → 504 Gateway Timeout
```

Your job:

> Find the root cause.

---

# 🧪 Investigation Plan

### Step 1

Check DNS:

```bash
dig example.com
```

---

### Step 2

Check HTTPS:

```bash
curl -v https://example.com
```

---

### Step 3

Check ALB target health.

---

### Step 4

Check EC2:

```bash
systemctl status <application>
```

---

### Step 5

Check listening ports:

```bash
ss -lntup
```

---

### Step 6

Check local application:

```bash
curl http://127.0.0.1:<PORT>
```

---

### Step 7

Check network access:

```bash
nc -vz <PRIVATE-IP> <PORT>
```

---

### Step 8

Check:

```text
Security Group
NACL
Route Table
```

---

### Step 9

Check application logs:

```bash
journalctl -u <service>
```

---

### Step 10

Check system/network evidence:

```bash
sudo tcpdump -i any port <PORT>
```

---

# 🧠 Incident Report

Document:

```text
Incident:
Production Website Down

Time:
02:15 AM

Impact:
Users unable to access website

Symptoms:
504 Gateway Timeout

Root Cause:
____________________

Evidence:
____________________

Fix:
____________________

Verification:
____________________

Preventive Action:
____________________
```

This is excellent practice for real DevOps work.

---

# 🔥 DevOps Connection

This chapter is extremely important because real DevOps isn't only:

```text
🚀 Deploy
```

It's also:

```text
🚨 Detect
   ↓
🔎 Investigate
   ↓
🧠 Diagnose
   ↓
🛠️ Fix
   ↓
✅ Verify
   ↓
📊 Monitor
   ↓
📝 Document
```

When production breaks, you need to understand:

```text
DNS
 ↓
IP
 ↓
Routing
 ↓
Firewall
 ↓
Load Balancer
 ↓
Server
 ↓
Port
 ↓
Application
 ↓
Database
```

And eventually:

```text
☁️ AWS
🐳 Docker
☸️ Kubernetes
🏗️ Terraform
🚀 CI/CD
📊 Prometheus
📈 Grafana
📝 ELK
```

all become part of the troubleshooting chain.

The biggest lesson:

> **Don't troubleshoot by guessing. Troubleshoot by narrowing the problem down with evidence.**

---

# 📚 Navigation

⬅️ Previous: **[16-Network-Security.md](16-Network-Security.md)**

➡️ Next: **[18-Networking-Hands-on-Labs.md](18-Networking-Hands-on-Labs.md)**

🏠 Networking Phase: **[README.md](README.md)**

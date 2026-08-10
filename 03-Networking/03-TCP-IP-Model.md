# 🌐 TCP/IP Model

## 🎯 What Are We Learning?

In the previous topic, we learned the **OSI Model**.

Now let's look at the model that is much closer to how the Internet actually works:

> **The TCP/IP Model.**

Think of OSI as a detailed **map for learning networking**, while TCP/IP is much closer to the **actual road system used by the Internet**. 🛣️

As a DevOps Engineer, you'll constantly encounter:

```text
TCP
IP
HTTP
HTTPS
DNS
SSH
UDP
Ethernet
Wi-Fi
```

Understanding how these fit together will make Docker, Kubernetes, AWS and troubleshooting much easier later.

---

# 🧠 What Is TCP/IP?

TCP/IP stands for:

```text
Transmission Control Protocol /
Internet Protocol
```

TCP/IP is a collection of networking protocols that enables computers and networks to communicate.

It is the foundation of the Internet.

Think:

```text
🌍 Internet
     ↓
   TCP/IP
     ↓
💻 Computer ↔ 🖥️ Server
```

---

# 🏠 Real-Life Example

Imagine sending a parcel from Pune to Delhi.

You need different things:

```text
📝 What are you sending?
        ↓
🚚 How should it be transported?
        ↓
📍 Where is it going?
        ↓
🛣️ Which network/road should it use?
```

Networking has similar responsibilities.

```text
Application
    ↓
Transport
    ↓
Internet
    ↓
Network Access
```

These are the four commonly used TCP/IP layers.

---

# 🏗️ The 4 TCP/IP Layers

```text
┌──────────────────────────────┐
│ 4️⃣ Application              │
├──────────────────────────────┤
│ 3️⃣ Transport                │
├──────────────────────────────┤
│ 2️⃣ Internet                 │
├──────────────────────────────┤
│ 1️⃣ Network Access           │
└──────────────────────────────┘
```

Let's meet them.

---

# 4️⃣ Application Layer

## 🎯 What Does It Do?

The Application layer is where applications interact with network services.

Examples:

```text
HTTP
HTTPS
DNS
SSH
SMTP
FTP
```

Think:

> 🗣️ **"What does the application want to communicate?"**

---

# 🌐 Real-Life Example

You open your browser:

```text
https://youtube.com
```

Your browser needs to communicate with a web server.

It uses:

```text
HTTPS
```

The browser essentially says:

> "I want this resource."

The server responds.

```text
Browser
   ↓
HTTPS Request
   ↓
Web Server
   ↓
HTTPS Response
```

---

# 💻 Try It Yourself

Run:

```bash
curl -I https://example.com
```

You may see something like:

```text
HTTP/2 200
content-type: text/html
```

You're interacting with an **application-layer protocol**.

🔥 You're already using the TCP/IP model.

---

# 📡 Common Application Protocols

| Protocol | Purpose |
|---|---|
| HTTP | Web communication |
| HTTPS | Secure web communication |
| DNS | Name resolution |
| SSH | Secure remote access |
| SMTP | Sending email |
| FTP | File transfer |

---

# 3️⃣ Transport Layer

Now we need to figure out:

> "How should the data travel between applications?"

This is the job of the Transport layer.

The two big players are:

```text
TCP
UDP
```

---

# 🚚 TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP provides:

```text
Reliable communication
Ordered delivery
Error detection
Retransmission
Flow control
Connection management
```

Think of TCP like a courier service that says:

> "I'll make sure everything gets there, in the right order." 📦

---

# 📦 TCP Real-Life Example

Imagine sending:

```text
📦 Package 1
📦 Package 2
📦 Package 3
```

Suppose Package 2 gets lost.

TCP can detect the missing data and retransmit it.

```text
📦 1 → ✅
📦 2 → ❌
📦 3 → ✅

       ↓

📦 2 → 🔄 Resent
```

This makes TCP useful when reliable delivery matters.

---

# 🌊 UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP is connectionless and does not provide TCP's built-in reliability, ordering, or retransmission mechanisms.

Think:

> "Just send it quickly; don't wait around for confirmations." 😄

---

# 🏎️ UDP Real-Life Example

Imagine a live gaming or voice communication scenario.

You may care more about:

```text
⚡ Low latency
```

than retransmitting every missing packet.

A late packet may be useless anyway.

That's one reason UDP is useful for real-time applications.

---

# 🆚 TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Built-in | No built-in reliability |
| Ordering | Yes | No built-in ordering |
| Retransmission | Yes | No |
| Flow Control | Yes | No TCP-style flow control |
| Overhead | Higher | Lower |
| Typical Use | Web, SSH | DNS, real-time traffic |

> ⚠️ UDP applications can implement their own reliability mechanisms when required.

---

# 🚪 Ports

Here's an important concept.

Imagine a building:

```text
🏢 IP Address = Building
🚪 Port = Door
⚙️ Service = Person behind the door
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

Port 22 is commonly used by SSH.

---

# 🔎 Find Ports on Linux

Run:

```bash
ss -lntup
```

You might see:

```text
LISTEN
0.0.0.0:22
```

This means a service is listening for connections on port 22.

🎮 **Challenge:**

Find one listening TCP port on your machine.

Write:

```text
Port:
Protocol:
Service:
```

---

# 2️⃣ Internet Layer

Now we need to answer:

> "Where should this packet go?"

That's the job of the Internet layer.

The major protocol here is:

```text
IP
```

Including:

```text
IPv4
IPv6
```

---

# 🏠 Real-Life Example

Imagine sending a parcel.

You write:

```text
Receiver:
Shubham
Pune
Maharashtra
India
```

The address helps the delivery network determine where the parcel needs to go.

Similarly, IP addressing provides:

```text
Source IP
Destination IP
```

Example:

```text
Source:
192.168.1.10

Destination:
8.8.8.8
```

---

# 🛣️ Routing

Routers use routing information to determine where packets should be forwarded.

Think:

```text
💻 Laptop
    ↓
📡 Router
    ↓
🛣️ Network
    ↓
📡 Router
    ↓
🖥️ Server
```

On Linux:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

This tells the machine where to send traffic when there isn't a more specific route.

---

# 🔍 Try It Yourself

Run:

```bash
ip addr
```

Then:

```bash
ip route
```

Find:

```text
Your IP:
Your interface:
Default route:
Gateway:
```

---

# 📦 What Is an IP Packet?

At the Internet layer, data is carried in an IP packet.

A simplified packet contains:

```text
┌─────────────────────────────┐
│ Source IP                   │
├─────────────────────────────┤
│ Destination IP              │
├─────────────────────────────┤
│ Protocol                    │
├─────────────────────────────┤
│ Data                        │
└─────────────────────────────┘
```

The router primarily cares about information such as:

```text
Destination IP
```

to make forwarding decisions.

---

# 1️⃣ Network Access Layer

This is where we deal with the local network technology used to actually transmit data.

It corresponds roughly to:

```text
OSI Layer 1
+
OSI Layer 2
```

Concepts include:

```text
Ethernet
Wi-Fi
MAC Addresses
Frames
Physical Media
Network Interfaces
```

---

# 🏠 Real-Life Example

Think about a delivery.

The Internet layer tells you:

> "This package needs to reach Delhi."

The Network Access layer is more like:

> "How do we move this package across this particular local road/link?"

For example:

```text
💻 Laptop
   ↓
📡 Wi-Fi
   ↓
📡 Router
```

or:

```text
💻 Server
   ↓
🔌 Ethernet
   ↓
🔀 Switch
```

---

# 🪪 MAC Address

At the local network level, devices use MAC addresses.

Run:

```bash
ip link
```

You may see:

```text
link/ether 00:11:22:33:44:55
```

That's a MAC address.

Remember:

```text
IP  → Logical addressing
MAC → Local network addressing
```

---

# 🆚 OSI vs TCP/IP

Now let's connect what you've learned.

## OSI

```text
7️⃣ Application
6️⃣ Presentation
5️⃣ Session
4️⃣ Transport
3️⃣ Network
2️⃣ Data Link
1️⃣ Physical
```

## TCP/IP

```text
4️⃣ Application
3️⃣ Transport
2️⃣ Internet
1️⃣ Network Access
```

---

# 🔄 Mapping the Models

```text
OSI MODEL                 TCP/IP MODEL

Application ──────────┐
Presentation ─────────┼──→ Application
Session ──────────────┘

Transport ───────────────→ Transport

Network ─────────────────→ Internet

Data Link ─────────────┐
Physical ──────────────┴──→ Network Access
```

---

# 🧠 Why Does TCP/IP Have Fewer Layers?

The OSI model separates:

```text
Application
Presentation
Session
```

into three layers.

TCP/IP commonly combines those responsibilities into:

```text
Application
```

Similarly:

```text
Data Link
Physical
```

are commonly grouped as:

```text
Network Access
```

So:

```text
OSI       = 7 layers
TCP/IP    = 4 layers
```

---

# 📦 Follow a Real Request

Let's see what happens when you run:

```bash
curl https://example.com
```

Simplified:

```text
1️⃣ Application
      ↓
HTTPS request

2️⃣ Transport
      ↓
TCP

3️⃣ Internet
      ↓
IP

4️⃣ Network Access
      ↓
Ethernet / Wi-Fi

5️⃣ 🌍 Network
      ↓
6️⃣ Remote Server
```

At the receiving side:

```text
Network Access
      ↓
Internet
      ↓
Transport
      ↓
Application
      ↓
Web Server
```

---

# 📦 Encapsulation

When data travels down the TCP/IP stack, each layer adds information.

Think of putting a letter into multiple envelopes.

```text
Application Data
       ↓
TCP Segment
       ↓
IP Packet
       ↓
Frame
       ↓
Bits
```

So:

```text
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Bits
```

---

# 📬 Decapsulation

At the destination, the process happens in reverse.

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Data
```

This is called:

```text
Decapsulation
```

---

# 🎮 Real-Life Challenge

Imagine you are sending a parcel.

Match the following:

```text
📦 Parcel contents
🏷️ Destination address
🚚 Transport method
🛣️ Local road
```

with:

```text
Application
Transport
Internet
Network Access
```

### Think first.

Answer:

```text
📦 Parcel contents     → Application
🚚 Transport method    → Transport
🏷️ Destination        → Internet
🛣️ Local road         → Network Access
```

Again, this is an analogy to build intuition—not a perfect one-to-one mapping.

---

# 🔧 Hands-on Lab

## Mission 1 — Find Your IP

```bash
ip addr
```

Record:

```text
IPv4:
IPv6:
Interface:
```

---

## Mission 2 — Find Your Route

```bash
ip route
```

Record:

```text
Default Gateway:
Default Interface:
```

---

## Mission 3 — Test IP Connectivity

```bash
ping 8.8.8.8
```

Think:

> Which TCP/IP layer is primarily involved?

Answer:

```text
Internet Layer
```

---

## Mission 4 — Test DNS

```bash
dig google.com
```

Think:

> Which TCP/IP layer does DNS belong to?

Answer:

```text
Application Layer
```

---

## Mission 5 — Test HTTPS

```bash
curl -I https://example.com
```

Think:

```text
Application → HTTPS
Transport   → TCP
Internet    → IP
Network     → Ethernet/Wi-Fi
```

---

## Mission 6 — Find Listening Ports

```bash
ss -lntup
```

Find:

```text
Port:
Protocol:
Process:
```

Ask:

> Which layer deals with TCP/UDP ports?

Answer:

```text
Transport Layer
```

---

# 🚨 Real DevOps Troubleshooting

Imagine your application isn't reachable.

You don't just randomly restart everything. 😄

Use the TCP/IP layers.

---

## 🔎 Application Layer

Question:

```text
Is the application responding?
```

Try:

```bash
curl
```

---

## 🔎 Transport Layer

Question:

```text
Is the required TCP/UDP port reachable?
```

Check:

```bash
ss -lntup
```

---

## 🔎 Internet Layer

Question:

```text
Does the machine have an IP?
Is the route correct?
```

Check:

```bash
ip addr
ip route
```

---

## 🔎 Network Access Layer

Question:

```text
Is the network interface working?
```

Check:

```bash
ip link
```

---

# 🧠 DevOps Example

Imagine this architecture:

```text
                    🌍 Internet
                         │
                         ↓
                     ⚖️ Load Balancer
                         │
                         ↓
                    🖥️ Server
                         │
                         ↓
                    🗄️ Database
```

A user says:

> "Website is down."

You investigate:

```text
DNS
 ↓
Application
 ↓
Port 443
 ↓
IP
 ↓
Routing
 ↓
Network Interface
```

TCP/IP knowledge helps you understand **where to look instead of guessing**.

---

# ☁️ TCP/IP in AWS

Later you'll build something like:

```text
🌍 Internet
     ↓
☁️ AWS
     ↓
🌐 VPC
     ↓
Public Subnet
     ↓
⚖️ ALB
     ↓
Private Subnet
     ↓
🖥️ Application
     ↓
🗄️ Database
```

You'll repeatedly encounter:

```text
IP Addresses
Subnets
Routes
Ports
TCP
UDP
DNS
Load Balancers
Security Groups
NAT
```

So this topic is directly connected to your future AWS work.

---

# 🐳 TCP/IP + Docker

Docker networking also uses the same fundamental concepts.

For example:

```text
Browser
   ↓
Host Port 8080
   ↓
Docker Container
   ↓
Container Port 80
   ↓
Nginx
```

You'll later learn:

```text
Docker Bridge Network
Port Mapping
Container IP
DNS
Network Isolation
```

---

# ☸️ TCP/IP + Kubernetes

Kubernetes takes networking to another level.

You'll eventually see:

```text
User
 ↓
Ingress
 ↓
Service
 ↓
Pod
 ↓
Container
```

And you'll need to understand:

```text
IP
Ports
TCP/UDP
DNS
Routing
Load Balancing
Network Policies
```

That's why we're building these foundations now.

---

# 🎮 Final Challenge

Imagine this request:

```text
curl https://myapp.com
```

Explain what happens using the TCP/IP model.

Try answering:

```text
1️⃣ Which layer handles HTTPS?

2️⃣ Which transport protocol is commonly used for HTTPS?

3️⃣ Which layer handles the destination IP?

4️⃣ Which layer handles Ethernet/Wi-Fi?

5️⃣ Which layer is responsible for TCP ports?

6️⃣ Which command can show your IP?

7️⃣ Which command can show your route?

8️⃣ Which command can show listening ports?
```

### Answers

```text
1. Application
2. TCP
3. Internet
4. Network Access
5. Transport
6. ip addr
7. ip route
8. ss -lntup
```

---

# 🧠 Remember This

Don't memorize TCP/IP as four boring boxes.

Think:

```text
🗣️ Application
"What do I want?"

🚚 Transport
"How should applications communicate?"

📍 Internet
"Where should this packet go?"

🔌 Network Access
"How do I send it across this network?"
```

Or simply:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Ethernet / Wi-Fi
```

That's the core idea.

---

# 💼 Interview Corner

### Q: What is the TCP/IP model?

> The TCP/IP model is a practical networking model used to describe communication across Internet-based networks. It is commonly represented using four layers: Application, Transport, Internet, and Network Access.

---

### Q: What are the four TCP/IP layers?

```text
Application
Transport
Internet
Network Access
```

---

### Q: What is the difference between OSI and TCP/IP?

> OSI is a seven-layer conceptual reference model, while TCP/IP is the practical protocol architecture used by modern Internet networking and is commonly represented using four layers.

---

### Q: Which layer does HTTP belong to?

```text
Application
```

---

### Q: Which layer does TCP belong to?

```text
Transport
```

---

### Q: Which layer does IP belong to?

```text
Internet
```

---

### Q: Where do Ethernet and Wi-Fi fit?

```text
Network Access
```

---

### Q: What is encapsulation?

> Encapsulation is the process of adding protocol-specific information as data moves down the networking stack.

Simplified:

```text
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
```

---

### Q: What is decapsulation?

> Decapsulation is the reverse process where protocol information is processed as data moves up the networking stack at the destination.

---

### Q: Why should a DevOps Engineer understand TCP/IP?

> Because cloud infrastructure, containers, Kubernetes, APIs, load balancers, CI/CD systems, monitoring, and production applications all depend on networking.

---

# 🏆 What You Should Be Able to Explain

Before moving to IPv4, make sure you can explain:

- [ ] What TCP/IP is
- [ ] Why TCP/IP is important
- [ ] The four TCP/IP layers
- [ ] What the Application layer does
- [ ] What the Transport layer does
- [ ] TCP vs UDP
- [ ] What ports are
- [ ] What the Internet layer does
- [ ] What IP addresses are
- [ ] What routing is
- [ ] What the Network Access layer does
- [ ] IP vs MAC
- [ ] OSI vs TCP/IP
- [ ] Encapsulation
- [ ] Decapsulation
- [ ] How `curl` uses networking
- [ ] How to inspect your Linux network
- [ ] How TCP/IP helps troubleshoot DevOps systems

---

# 🎯 Mini Assignment

Draw this without looking at the notes:

```text
              TCP/IP MODEL

        ┌──────────────────┐
        │   Application    │
        ├──────────────────┤
        │    Transport     │
        ├──────────────────┤
        │     Internet     │
        ├──────────────────┤
        │ Network Access   │
        └──────────────────┘
```

Then write at least **two examples** for each layer.

Example:

```text
Application → HTTP, DNS
Transport   → TCP, UDP
Internet    → IPv4, IPv6
Network     → Ethernet, Wi-Fi
```

If you can draw it and explain **why each protocol belongs there**, you've understood the topic—not just memorized it. 🔥

---

# 📚 Navigation

⬅️ Previous: **[02-OSI-Model.md](02-OSI-Model.md)**

➡️ Next: **[04-IPv4.md](04-IPv4.md)**

🏠 Networking Phase: **[README.md](README.md)**

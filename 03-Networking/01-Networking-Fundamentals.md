# 🌐 Networking Fundamentals

## 🎯 What Are We Learning?

Before jumping into OSI, TCP/IP, IP addresses, subnetting, DNS, routing, and all the other networking stuff, let's understand the big picture:

> **How does one computer actually talk to another computer?**

As a DevOps Engineer, you'll constantly deal with:

```text
💻 Servers
☁️ Cloud
🐳 Docker
☸️ Kubernetes
🌐 APIs
⚖️ Load Balancers
🔥 Firewalls
🔐 SSH
📡 DNS
```

And guess what?

**All of them depend on networking.**

---

# 🏠 Let's Start With Real Life

Imagine you order something online.

You give the delivery company:

```text
Your Name
Your House Address
```

The delivery person uses that address to find your house.

Computers work in a surprisingly similar way.

Instead of:

```text
🏠 House Address
```

we have:

```text
🌐 IP Address
```

Instead of:

```text
🚪 Different doors in a building
```

we have:

```text
🔢 Ports
```

Instead of:

```text
🚚 Delivery Person
```

we have:

```text
📦 Network Packets
```

So we can think of networking like this:

```text
🏠 Real World             💻 Networking

House Address      →      IP Address
Door               →      Port
Delivery Package   →      Packet
Road               →      Network
Traffic Police     →      Router
Security Guard     →      Firewall
Phone Directory    →      DNS
```

Pretty much the same game, just with fewer delivery guys. 😄

---

# 🌐 What Is a Network?

A network is simply a group of devices that can communicate with each other.

For example, your home might look like:

```text
              🌐 Internet
                   │
                   ↓
              📡 Router
              /    |    \
             /     |     \
           💻     📱     📺
        Laptop   Phone   TV
```

Your devices communicate through the network.

In a company:

```text
                    🌐 Internet
                         │
                         ↓
                     🔥 Firewall
                         │
                    ⚖️ Load Balancer
                    /          \
                   ↓            ↓
              🖥️ Server 1    🖥️ Server 2
                   \            /
                    \          /
                         ↓
                    🗄️ Database
```

And in cloud environments:

```text
🌍 Internet
     ↓
☁️ Cloud
     ↓
🌐 VPC
     ↓
⚖️ Load Balancer
     ↓
☸️ Kubernetes / 🖥️ EC2
     ↓
🗄️ Database
```

This is why networking becomes **very important in DevOps**.

---

# 🧩 The Main Characters

Let's meet the important networking components.

---

## 💻 Client

The **client** asks for something.

Examples:

```text
🌐 Browser
📱 Mobile App
💻 curl
🧪 API Client
```

Example:

You open:

```text
https://google.com
```

Your browser is the client.

---

## 🖥️ Server

The **server** provides something.

For example:

```text
Client → "Give me this webpage."

Server → "Here you go!"
```

A server could be:

```text
🌐 Web Server
⚙️ Application Server
🗄️ Database Server
📡 DNS Server
📧 Mail Server
```

---

# 🔀 Switch

Imagine an office with 20 computers.

You don't want to connect every computer directly to every other computer.

Instead:

```text
💻 ──┐
💻 ──┤
💻 ──┼── 🔀 Switch
💻 ──┤
🖥️ ──┘
```

A switch connects devices within a local network.

Think:

> **Switch = office receptionist connecting people inside the building.**

---

# 🌐 Router

Now imagine your laptop wants to communicate with a server somewhere on the Internet.

Your laptop can't directly connect to every network in the world.

So it asks the router:

> "Hey, I need to send this traffic outside our network."

The router figures out where to send it.

```text
💻 Laptop
    ↓
📡 Router
    ↓
🌐 Internet
    ↓
🖥️ Server
```

Think:

> **Router = traffic controller that helps packets find their next destination.**

---

# 🔥 Firewall

Imagine an office building with a security guard.

Someone arrives and says:

> "I'm here to enter through Door 22."

The security guard checks the rules.

```text
Allowed?  → 🚪 Let them in
Blocked?  → 🛑 Stop them
```

A firewall does something similar with network traffic.

Example:

```text
SSH : 22
HTTPS : 443
HTTP : 80
```

A firewall can have rules such as:

```text
Allow HTTPS
Allow SSH from trusted IP
Block everything else
```

Think:

> **Firewall = security guard for network traffic.**

---

# 📦 So What Actually Travels Through the Network?

Computers don't send one giant blob of data.

Data is broken into smaller units as it moves through the networking stack.

A simplified view:

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

Don't worry about memorizing this yet.

We'll break it down properly when we study the **OSI Model** and **TCP/IP Model**.

---

# 🏗️ The OSI Model

Here's where networking starts getting interesting.

The OSI model gives us **7 layers** to understand how communication happens.

```text
7️⃣ Application
6️⃣ Presentation
5️⃣ Session
4️⃣ Transport
3️⃣ Network
2️⃣ Data Link
1️⃣ Physical
```

Think of sending a parcel.

There are different stages:

```text
📝 Prepare the information
      ↓
📦 Package it
      ↓
🏷️ Add addressing information
      ↓
🚚 Transport it
      ↓
🛣️ Move it through networks
      ↓
🏠 Deliver it
```

The OSI model gives us a structured way to understand these stages.

We'll study it properly in:

```text
02-OSI-Model.md
```

---

# 🌐 TCP/IP Model

The Internet doesn't actually run according to a magical seven-layer OSI checklist.

In practice, we use the **TCP/IP networking model**.

A common representation is:

```text
Application
     ↓
Transport
     ↓
Internet
     ↓
Network Access
```

We'll go deeper into this in:

```text
03-TCP-IP-Model.md
```

---

# 🏠 IP Address

Now let's meet one of the most important characters:

## 🌐 IP Address

Think about your home.

If someone wants to send you something, they need your address.

Similarly, computers need addresses.

Example:

```text
192.168.1.10
```

That's an IPv4 address.

So:

```text
🏠 House Address
      ↓
🌐 IP Address
```

---

# 🔍 Let's Find YOUR IP Address

Enough theory.

Open your Linux terminal and run:

```bash
ip addr
```

Look for something similar to:

```text
inet 192.168.x.x
```

You can also try:

```bash
hostname -I
```

### 🎮 Your Challenge

Find:

```text
Your IPv4 address:
Your network interface:
```

Don't just memorize what an IP address is.

**Find your own.**

---

# 🚪 Ports

Here's another important concept.

Imagine a large apartment building.

The building has an address:

```text
192.168.1.10
```

But inside the building there are many doors.

```text
🏢 Building
│
├── 🚪 22   → SSH
├── 🚪 80   → HTTP
└── 🚪 443  → HTTPS
```

So:

```text
IP Address = Building
Port       = Door
Service    = Person behind the door
```

For example:

```text
192.168.1.10:22
```

means:

> Connect to port 22 on the machine with IP `192.168.1.10`.

---

# 🔎 Let's See Your Open Doors

Run:

```bash
ss -lntup
```

You may see something like:

```text
LISTEN
0.0.0.0:22
127.0.0.1:631
```

Now ask yourself:

> "What services are listening on my machine?"

That's already real Linux troubleshooting.

---

# 🌍 IPv4 vs IPv6

There are two major versions of IP:

```text
IPv4
IPv6
```

IPv4 example:

```text
192.168.1.10
```

IPv6 example:

```text
2001:db8::1
```

Think:

```text
IPv4 → Older addressing system
IPv6 → Newer, much larger addressing system
```

We'll explore both separately:

```text
04-IPv4.md
05-IPv6.md
```

---

# 🧩 Subnetting

Now imagine your company has:

```text
1000 employees
```

You don't necessarily want everyone sitting in one giant network.

You might divide the network:

```text
Company Network
│
├── 👨‍💻 Developers
├── 🔐 Security
├── 🗄️ Databases
└── 🖥️ Infrastructure
```

This is where **subnetting** comes in.

Subnetting lets us divide a larger network into smaller networks.

Example:

```text
10.0.0.0/24
```

We'll learn how to calculate these properly in:

```text
06-Subnetting.md
```

---

# 🛣️ Routing

Imagine you're driving from:

```text
Pune → Delhi
```

You don't randomly drive around.

You follow routes.

Networks work similarly.

```text
💻 Source
   ↓
📡 Router
   ↓
🛣️ Route
   ↓
📡 Router
   ↓
🖥️ Destination
```

Linux can show its routing table:

```bash
ip route
```

You might see:

```text
default via 192.168.1.1
```

That basically tells your machine:

> "If you don't know where else to send this traffic, send it here."

We'll explore routing properly in:

```text
07-Routing.md
```

---

# 🔄 NAT

Here's a real-life problem.

Imagine your home has:

```text
💻 Laptop
📱 Phone
📺 TV
```

All of them use private IP addresses.

But the Internet needs a public-facing address.

NAT helps translate between these address spaces.

```text
💻 192.168.1.10 ──┐
📱 192.168.1.11 ──┼── 📡 Router/NAT ── 🌐 Internet
📺 192.168.1.12 ──┘
```

Think:

> **NAT = translator between private and public addressing.**

We'll explore it in:

```text
08-NAT.md
```

---

# 📡 Network Protocols

Computers need rules to communicate.

These rules are called **protocols**.

Some important ones:

```text
🌐 HTTP
🔒 HTTPS
🔐 SSH
📡 DNS
📦 DHCP
📁 FTP
📧 SMTP
```

Think of protocols as:

> **"Rules of the conversation."**

For example:

```text
HTTP

Client:
"GET /index.html"

Server:
"200 OK"
```

We'll cover these in:

```text
09-Network-Protocols.md
```

---

# 🐧 Networking on Linux

Now let's make this practical.

Linux gives us tools to investigate networking.

Here are the ones you'll use a lot:

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

Suppose your friend isn't answering their phone.

You might ask:

> "Are they reachable?"

`ping` does something conceptually similar.

Try:

```bash
ping 8.8.8.8
```

Then:

```bash
ping google.com
```

Stop it with:

```text
Ctrl + C
```

---

# 🎮 Mini Challenge

Try:

```bash
ping 127.0.0.1
```

Then:

```bash
ping 8.8.8.8
```

Then:

```bash
ping google.com
```

Now ask:

```text
Which one checks my own machine?
Which one checks an external IP?
Which one also requires DNS resolution?
```

Don't worry if you're not 100% sure yet.

We'll revisit this during troubleshooting.

---

# 🔍 `dig`

Remember DNS?

Let's actually use it.

Run:

```bash
dig google.com
```

You'll get DNS information.

Try:

```bash
dig google.com A
```

Then:

```bash
dig google.com AAAA
```

Now you're not just learning:

> "DNS converts names to IP addresses."

You're actually **asking DNS a question**.

---

# 🌐 `curl`

`curl` is one of your future DevOps best friends.

Try:

```bash
curl https://example.com
```

You just made an HTTP request from your terminal.

Want only the headers?

```bash
curl -I https://example.com
```

Want to see what's happening underneath?

```bash
curl -v https://example.com
```

This becomes extremely useful later for:

```text
API Testing
Health Checks
CI/CD
Kubernetes Troubleshooting
Cloud Troubleshooting
```

---

# 🔌 `ss`

Remember our building analogy?

```text
🏢 IP Address
🚪 Ports
```

Let's see which doors are open.

Run:

```bash
ss -lntup
```

Look at:

```text
Local Address
Port
Process
```

You're basically asking Linux:

> "Which services are listening for network connections?"

---

# ☁️ Networking in DevOps

Now let's connect everything to your career.

Imagine you're deploying an application to AWS.

You might eventually have:

```text
                    🌍 Internet
                         │
                         ↓
                      🌐 DNS
                         │
                         ↓
                   ⚖️ Load Balancer
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
        🖥️ App Server 1       🖥️ App Server 2
              │                     │
              └──────────┬──────────┘
                         ↓
                    🗄️ Database
```

There are networking concepts everywhere:

```text
DNS
IP
Ports
Routing
Subnets
Firewalls
Load Balancing
NAT
```

Later, you'll see the same concepts in:

```text
🐳 Docker
☸️ Kubernetes
☁️ AWS
🏗️ Terraform
🔄 CI/CD
🏢 Platform Engineering
```

---

# ☸️ Networking + Kubernetes

Kubernetes makes networking even more interesting.

Eventually you'll see:

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

You'll need to understand:

```text
IP addresses
Ports
DNS
Routing
Load Balancing
Network Policies
```

So the networking you're learning **right now** isn't random theory.

It's preparing you for Kubernetes.

---

# 🧠 A Real DevOps Scenario

Imagine your manager messages you:

> 🚨 "The application is down. Users can't access it."

Don't immediately restart everything. 😅

Think like a DevOps Engineer.

Start asking:

```text
1️⃣ Does the server have an IP?
        ↓
2️⃣ Is the network interface working?
        ↓
3️⃣ Is there a route?
        ↓
4️⃣ Can we reach the destination?
        ↓
5️⃣ Is DNS working?
        ↓
6️⃣ Is the required port open?
        ↓
7️⃣ Is the service running?
        ↓
8️⃣ Is the application responding?
```

Commands might include:

```bash
ip addr
```

```bash
ip route
```

```bash
ping
```

```bash
dig
```

```bash
ss
```

```bash
curl
```

This is the beginning of **real production troubleshooting**.

---

# 🧪 Your First Networking Mission

Don't just read this section.

Open your WSL/Linux terminal.

### Mission 1 — Find Your Address

```bash
hostname -I
```

Write down:

```text
My IP:
```

---

### Mission 2 — Find Your Interface

```bash
ip addr
```

Find the interface carrying your IP.

Write:

```text
Interface:
```

---

### Mission 3 — Find Your Route

```bash
ip route
```

Find:

```text
Default Gateway:
```

---

### Mission 4 — Test Yourself

```bash
ping 127.0.0.1
```

---

### Mission 5 — Test the Internet

```bash
ping 8.8.8.8
```

---

### Mission 6 — Test DNS

```bash
ping google.com
```

---

### Mission 7 — Ask DNS

```bash
dig google.com
```

If `dig` isn't installed:

```bash
sudo apt install dnsutils
```

---

### Mission 8 — Talk HTTP

```bash
curl -I https://example.com
```

---

### Mission 9 — Check Your Doors

```bash
ss -lntup
```

---

# 🎮 Final Challenge

Without looking at the explanations above, explain this:

```text
💻 Your Laptop
      ↓
📡 Router
      ↓
🌐 Internet
      ↓
📡 Router
      ↓
⚖️ Load Balancer
      ↓
🖥️ Application Server
```

Answer these questions:

```text
1. What identifies the destination machine?
2. What identifies a service on that machine?
3. Who decides where packets should go?
4. What translates private/public addresses?
5. What translates domain names?
6. What protects traffic using network rules?
7. What tool can test basic connectivity?
8. What tool can test HTTP?
9. What tool can inspect DNS?
10. What command shows Linux routing information?
```

If you can answer those without memorizing a paragraph, you're learning this correctly. 🔥

---

# 💼 Interview Corner

### Q: What is networking?

**Answer:**

> Networking is the communication between devices using defined protocols and addressing mechanisms to exchange data.

---

### Q: What is an IP address?

**Answer:**

> An IP address is a logical address used to identify a network interface and enable communication across IP networks.

---

### Q: What is a port?

**Answer:**

> A port identifies a service endpoint associated with a transport-layer protocol on a host.

---

### Q: What does a router do?

**Answer:**

> A router forwards packets between different networks using routing information.

---

### Q: What does DNS do?

**Answer:**

> DNS resolves domain names into IP addresses and provides other DNS information.

---

### Q: How would you troubleshoot a server that cannot reach the Internet?

Start from the bottom and move upward:

```text
Interface
   ↓
IP Address
   ↓
Routing
   ↓
Connectivity
   ↓
DNS
   ↓
Port
   ↓
Application
```

Useful commands:

```bash
ip addr
ip route
ping
dig
ss
curl
```

---

# 🧠 Remember This

Don't try to memorize 50 networking definitions.

Remember this picture:

```text
                 🌍 INTERNET
                      │
                      ↓
                  🛣️ ROUTING
                      │
                      ↓
                 🌐 IP ADDRESS
                      │
                      ↓
                   🚪 PORT
                      │
                      ↓
                ⚙️ SERVICE
                      │
                      ↓
                📦 APPLICATION
```

And remember:

```text
🌐 IP       → Where?
🚪 Port     → Which service?
📡 Router   → Where next?
🔎 DNS      → What IP belongs to this name?
🔥 Firewall → Should this traffic be allowed?
⚖️ LB       → Which backend should receive it?
```

---

# 🎯 Learning Outcome

After completing this topic, you should be able to:

- [ ] Explain what networking is
- [ ] Explain clients and servers
- [ ] Explain switches
- [ ] Explain routers
- [ ] Explain firewalls
- [ ] Understand the purpose of the OSI model
- [ ] Understand the purpose of the TCP/IP model
- [ ] Understand IP addresses
- [ ] Understand ports
- [ ] Explain the purpose of DNS
- [ ] Explain routing
- [ ] Explain NAT
- [ ] Identify common networking protocols
- [ ] Use `ip`
- [ ] Use `ping`
- [ ] Use `curl`
- [ ] Use `dig`
- [ ] Use `ss`
- [ ] Perform basic network troubleshooting
- [ ] Explain why networking matters in DevOps

---

# 📚 Navigation

⬅️ Previous: **[Networking README](README.md)**

➡️ Next: **[02-OSI-Model.md](02-OSI-Model.md)**

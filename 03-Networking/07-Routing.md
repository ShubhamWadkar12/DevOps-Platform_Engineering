# 🛣️ Routing

## 🎯 What Are We Learning?

Imagine you're driving from:

```text
📍 Pune
   ↓
📍 Mumbai
   ↓
📍 Surat
   ↓
📍 Delhi
```

You don't just drive randomly.

At every major junction, you need to know:

> **"Which road should I take next?"**

Computer networks have the same problem.

When a packet needs to travel from one network to another, **routers make forwarding decisions** based on routing information.

That's routing.

> **Routing = deciding where network traffic should be forwarded to reach its destination.**

---

# 🏠 Real-Life Analogy

Imagine sending a parcel:

```text
📦 Your House
      ↓
🏤 Local Delivery Center
      ↓
🏤 Regional Center
      ↓
🏤 Delhi Center
      ↓
🏠 Destination
```

Each delivery center decides:

> "Where should this package go next?"

A router does something conceptually similar:

```text
📦 Packet
   ↓
📡 Router
   ↓
📡 Next Hop
   ↓
📡 Next Router
   ↓
🖥️ Destination
```

The router doesn't necessarily know the entire journey as one fixed road.

It makes a forwarding decision based on its routing information.

---

# 🌐 What Is Routing?

Routing is the process of determining a path for packets between networks.

For example:

```text
Network A
192.168.1.0/24
       ↓
     Router
       ↓
Network B
10.0.0.0/24
```

The router needs to know:

```text
10.0.0.0/24
      ↓
Where should I send traffic?
```

---

# 🔀 Routing vs Forwarding

These terms are related but not exactly the same.

### Routing

> **Routing is the process of determining paths and building routing information.**

### Forwarding

> **Forwarding is the actual process of sending a packet toward the selected next hop/interface.**

Think:

```text
🧠 Routing
"Which road should we use?"

🚗 Forwarding
"Okay, take this road."
```

---

# 🧩 Why Do We Need Routers?

A switch is mainly used to connect devices within a local network.

A router connects different IP networks.

For example:

```text
Network A
192.168.1.0/24
     │
     │
   🔀 Switch
     │
     ↓
   📡 Router
     │
     ↓
Network B
10.0.0.0/24
```

Think:

```text
🔀 Switch
→ Connects devices on a local network

📡 Router
→ Connects different networks
```

---

# 🌐 Example

Suppose:

```text
Laptop:
192.168.1.10/24

Server:
10.0.0.10/24
```

These are different networks.

The laptop cannot simply treat the server as another local host.

Traffic generally needs a Layer 3 forwarding device:

```text
💻 Laptop
192.168.1.10
     ↓
📡 Router
     ↓
🖥️ Server
10.0.0.10
```

---

# 🧠 The Routing Table

A router needs routing information.

Linux machines also have routing tables.

Run:

```bash
ip route
```

You may see something like:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.10
```

Let's break this down.

---

# 🔍 Reading a Route

Example:

```text
192.168.1.0/24 dev eth0
```

This means:

```text
Destination:
192.168.1.0/24

Interface:
eth0
```

Linux knows that this network is directly connected through:

```text
eth0
```

---

# 🚪 Default Route

You may also see:

```text
default via 192.168.1.1 dev eth0
```

This is extremely important.

It means:

> "If there isn't a more specific route for the destination, send the traffic to `192.168.1.1`."

Think:

```text
Specific destination known?
        │
       YES
        ↓
Use specific route

       NO
        ↓
Use default route
```

---

# 🏠 Real-Life Example

Imagine a delivery office.

You have specific instructions:

```text
Pune → Road A
Mumbai → Road B
Delhi → Road C
```

But what if nobody knows the destination?

You have a default instruction:

```text
"Send it to the main regional center."
```

That's similar to a default route.

---

# 🛣️ Default Gateway

On a typical local network, the default route often points to a router that acts as the host's **default gateway**.

Example:

```text
Laptop:
192.168.1.10

Gateway:
192.168.1.1
```

Routing table:

```text
default via 192.168.1.1
```

Traffic destined for networks not otherwise covered by a more specific route can be sent to that gateway.

---

# 🔧 Find Your Default Gateway

Run:

```bash
ip route
```

Look for:

```text
default via X.X.X.X
```

For example:

```text
default via 192.168.1.1 dev eth0
```

Record:

```text
Default Gateway:
Interface:
```

---

# 🧩 Directly Connected Networks

Suppose your machine has:

```text
IP:
192.168.1.10/24
```

Your local network is:

```text
192.168.1.0/24
```

Linux knows this network is directly connected.

You may see:

```text
192.168.1.0/24 dev eth0
```

No external router is needed to determine the local Layer 2 destination.

---

# 🧭 Routing Decision

Suppose your machine wants to communicate with:

```text
192.168.1.20
```

Your machine has:

```text
192.168.1.0/24
```

The destination is inside the local subnet.

So:

```text
💻
 ↓
🔀 Local Network
 ↓
🖥️ 192.168.1.20
```

But suppose the destination is:

```text
8.8.8.8
```

That's not inside:

```text
192.168.1.0/24
```

So the machine needs another route, often:

```text
default
   ↓
192.168.1.1
```

Then:

```text
💻 Laptop
    ↓
📡 Default Gateway
    ↓
🌍 Internet
```

---

# 🎯 Longest Prefix Match

This is one of the most important routing concepts.

Imagine your routing table contains:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

And the destination is:

```text
10.10.10.50
```

Which route should be selected?

All three technically match.

But the most specific route is:

```text
10.10.10.0/24
```

because `/24` is a longer prefix than `/16` or `/8`.

This is called:

> **Longest Prefix Match**

Think:

```text
10.0.0.0/8
       ↓
Broad road

10.10.0.0/16
       ↓
More specific road

10.10.10.0/24
       ↓
Very specific road
```

The router chooses the most specific matching route.

---

# 🎮 Mini Challenge

Routing table:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
default
```

Destination:

```text
10.10.10.25
```

Which route wins?

### Answer:

```text
10.10.10.0/24
```

Because it is the most specific matching route.

---

# 🧩 Static Routing

A static route is manually configured.

Imagine telling a delivery driver:

> "For everything going to Network B, use this road."

Example concept:

```text
Destination:
10.20.0.0/16

Next Hop:
192.168.1.1
```

In Linux, a route can be added with:

```bash
sudo ip route add 10.20.0.0/16 via 192.168.1.1
```

⚠️ Only run route-changing commands when you understand the network you're working on. A wrong route can break connectivity.

---

# 🔄 Removing a Route

A route added manually can be removed with:

```bash
sudo ip route del 10.20.0.0/16 via 192.168.1.1
```

Again:

> 🛑 Don't experiment with route changes on a machine where you need network access unless you know how to recover.

For our learning, inspecting routes is enough unless you're working inside a controlled lab.

---

# 🤖 Dynamic Routing

Manually configuring every route doesn't scale.

Imagine:

```text
🌍 1000 Routers
```

Would you manually configure every path?

Absolutely not. 😂

Dynamic routing protocols allow routers to exchange routing information.

Examples:

```text
OSPF
BGP
EIGRP
IS-IS
RIP
```

For your DevOps journey, the most important ones to recognize are:

```text
OSPF
BGP
```

---

# 🧠 OSPF

OSPF stands for:

```text
Open Shortest Path First
```

It is an interior gateway protocol commonly used within an organization or autonomous system.

It allows routers to exchange information about network topology and calculate paths.

Think:

```text
🏢 Company Network

Router A ─── Router B
   │            │
   └── Router C ┘
```

Routers share topology information and calculate suitable paths.

---

# 🌍 BGP

BGP stands for:

```text
Border Gateway Protocol
```

BGP is the primary routing protocol used to exchange routing information between autonomous systems on the Internet.

Think:

```text
🏢 ISP A
   │
   │ BGP
   ↓
🏢 ISP B
   │
   ↓
🏢 ISP C
```

BGP is one of the reasons the global Internet can operate as a collection of interconnected networks.

---

# 🆚 Static vs Dynamic Routing

| Feature | Static | Dynamic |
|---|---|---|
| Configuration | Manual | Learned/exchanged |
| Automation | Low | Higher |
| Adaptation | Manual changes | Can adapt |
| Small networks | Useful | Useful |
| Large networks | Difficult | More suitable |
| Example | Static route | OSPF / BGP |

---

# 🌐 Routing Protocol Categories

A useful high-level distinction:

```text
IGP
↓
Routing inside an organization/autonomous system

EGP
↓
Routing between autonomous systems
```

Examples:

```text
IGP → OSPF, IS-IS
BGP → Inter-domain routing
```

---

# 🧩 Next Hop

Suppose:

```text
Laptop
192.168.1.10

Router
192.168.1.1

Destination
10.0.0.10
```

The laptop doesn't necessarily need to know every router between itself and the destination.

It may simply know:

```text
10.0.0.0/24
     ↓
Next Hop:
192.168.1.1
```

That router becomes the next hop.

Think:

```text
📦 Package
 ↓
🚚 Next delivery center
 ↓
🚚 Next delivery center
 ↓
🏠 Destination
```

---

# 🧭 Route Metrics

Sometimes multiple routes can reach the same destination.

A routing system may use a metric or preference to choose between them.

Think:

```text
Road A
10 km
Fast

Road B
20 km
Slow
```

The routing system needs a way to determine which path is preferred.

The exact metric depends on the routing protocol or routing implementation.

---

# 🔥 Routing vs Switching

This is a common interview question.

## Switching

Usually works primarily at:

```text
Layer 2
```

and uses information such as:

```text
MAC addresses
```

## Routing

Works at:

```text
Layer 3
```

and uses:

```text
IP addresses
```

Think:

```text
🔀 Switch
"Which device on this local network?"

📡 Router
"Which network should this packet go to?"
```

---

# 🏠 Real-Life Network

Imagine your home:

```text
                 🌍 Internet
                      │
                      ↓
                 📡 Router
                /    |    \
               /     |     \
             💻     📱     📺
```

Your router handles traffic between:

```text
🏠 Home Network
       ↕
🌍 Internet
```

Your switch or wireless access point handles local connectivity between devices.

---

# 🧪 Linux Routing Lab

Now let's investigate your actual Linux system.

---

## Mission 1 — View Routes

Run:

```bash
ip route
```

Write down:

```text
Default Route:
Local Network:
Interface:
Gateway:
```

---

## Mission 2 — IPv6 Routes

Run:

```bash
ip -6 route
```

Compare it with:

```bash
ip route
```

Notice that IPv4 and IPv6 maintain separate routing information.

---

# 🔎 Mission 3 — Find the Route to a Destination

Linux provides:

```bash
ip route get 8.8.8.8
```

You may see something similar to:

```text
8.8.8.8 via 192.168.1.1 dev eth0 src 192.168.1.10
```

This is extremely useful.

Linux is essentially telling you:

```text
Destination:
8.8.8.8

Next Hop:
192.168.1.1

Interface:
eth0

Source IP:
192.168.1.10
```

🔥 This is a real troubleshooting command.

---

# 🎮 Mission 4 — Compare Destinations

Run:

```bash
ip route get 127.0.0.1
```

Then:

```bash
ip route get 8.8.8.8
```

Then:

```bash
ip route get 192.168.1.1
```

Your exact output will depend on your Linux/WSL networking configuration.

Try to identify:

```text
Interface
Source IP
Gateway / Next Hop
```

---

# 🔍 Mission 5 — Trace a Path

You can use:

```bash
traceroute google.com
```

If `traceroute` isn't installed:

```bash
sudo apt install traceroute
```

Then:

```bash
traceroute google.com
```

You may see multiple hops:

```text
1   Router
2   ISP
3   ISP
4   ...
5   Destination
```

Think:

> "Show me the major routing hops between me and the destination."

---

# 🌐 `traceroute` vs `ping`

These are different tools.

### `ping`

Answers:

> "Can I reach this destination, and how long does it take?"

```bash
ping google.com
```

### `traceroute`

Answers:

> "What path/hops are visible between me and the destination?"

```bash
traceroute google.com
```

Think:

```text
ping
📍 "Can I get there?"

traceroute
🛣️ "Which way am I getting there?"
```

---

# 🧪 WSL Note

Because you're learning Linux through WSL, your network may look different from a normal physical Ubuntu machine.

You might see:

```text
eth0
```

with an internal WSL address and a gateway.

That's completely normal.

Don't compare your exact IP with someone else's machine.

Focus on understanding:

```text
Interface
IP
Route
Gateway
Destination
```

---

# ☁️ Routing in AWS

Now let's connect this to your DevOps career.

Imagine an AWS VPC:

```text
☁️ VPC
10.0.0.0/16
│
├── Public Subnet
│      10.0.1.0/24
│
└── Private Subnet
       10.0.2.0/24
```

You may have:

```text
🌍 Internet
    ↓
Internet Gateway
    ↓
Public Route Table
    ↓
Public Subnet
```

And:

```text
Private Subnet
      ↓
NAT Gateway
      ↓
Internet
```

Routing tables determine where traffic should go.

---

# 🏗️ AWS Route Tables

An AWS route table might conceptually contain:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

Meaning:

```text
10.0.0.0/16
      ↓
Keep traffic inside the VPC

0.0.0.0/0
      ↓
Send other traffic toward the Internet Gateway
```

This is the same fundamental routing concept you've just learned on Linux.

---

# 🐳 Routing + Docker

Docker creates virtual networks.

Conceptually:

```text
Host
│
├── Docker Network
│      │
│      ├── Container A
│      └── Container B
│
└── External Network
```

Traffic may move through:

```text
Container
   ↓
Docker Network
   ↓
Host/NAT
   ↓
External Network
```

Routing is part of understanding how containers communicate.

---

# ☸️ Routing + Kubernetes

Kubernetes networking gets even more interesting.

You can have:

```text
User
 ↓
Ingress
 ↓
Service
 ↓
Pod
```

Behind the scenes:

```text
Node
Pod Network
Service Network
External Network
```

The exact routing behavior depends on the Kubernetes networking implementation and CNI.

You'll later learn:

```text
CNI
Pod CIDR
Service CIDR
Network Policies
Ingress
Load Balancing
```

---

# 🚨 Real DevOps Troubleshooting Scenario

Imagine:

```text
Application Server:
10.0.2.20
```

Your teammate says:

> "I can't reach it from another server."

You investigate.

### Step 1 — Check local IP

```bash
ip addr
```

### Step 2 — Check routes

```bash
ip route
```

### Step 3 — Check the route to the server

```bash
ip route get 10.0.2.20
```

### Step 4 — Test connectivity

```bash
ping 10.0.2.20
```

### Step 5 — Check the application port

```bash
ss -lntup
```

### Step 6 — Test the application

```bash
curl http://10.0.2.20
```

Now you're troubleshooting systematically:

```text
IP
 ↓
Route
 ↓
Next Hop
 ↓
Connectivity
 ↓
Port
 ↓
Application
```

That's DevOps thinking. 🔥

---

# 🎮 Final Routing Challenge

You have this network:

```text
             🌍 Internet
                  │
                  ↓
             📡 Router A
             /         \
            /           \
     Network A         Network B
   192.168.1.0/24    10.0.0.0/24
        │                  │
       💻                 🖥️
```

Your laptop:

```text
192.168.1.10
```

Server:

```text
10.0.0.10
```

Question:

> Can the laptop directly treat the server as a local Layer 2 neighbor?

Answer:

```text
No.
```

Why?

Because:

```text
192.168.1.0/24
```

and:

```text
10.0.0.0/24
```

are different IP networks.

Traffic needs Layer 3 routing.

---

# 🎮 Final Challenge 2

Routing table:

```text
10.0.0.0/8
10.10.0.0/16
10.10.20.0/24
0.0.0.0/0
```

Destination:

```text
10.10.20.50
```

Which route wins?

Think:

```text
/8
/16
/24
/0
```

### Answer:

```text
10.10.20.0/24
```

Because of:

> **Longest Prefix Match**

---

# 🧠 Remember This

Don't memorize routing as:

> "Routers forward packets."

Understand the story:

```text
📦 Packet
   ↓
❓ Where does it need to go?
   ↓
📖 Check routing table
   ↓
🎯 Find best matching route
   ↓
🚪 Choose next hop/interface
   ↓
📡 Forward packet
```

And remember:

```text
🌐 IP Address
→ Where?

📖 Routing Table
→ What path?

🚪 Next Hop
→ Where next?

📡 Interface
→ Which network connection?

🏠 Default Route
→ Where should unknown destinations go?

🎯 Longest Prefix Match
→ Which matching route is most specific?
```

---

# 💼 Interview Corner

### Q: What is routing?

> Routing is the process of determining paths and forwarding traffic between different IP networks.

---

### Q: What is a routing table?

> A routing table contains information that a host or router uses to determine where packets destined for different networks should be forwarded.

---

### Q: What is a default route?

> A default route is used when no more specific route matches the destination.

IPv4:

```text
0.0.0.0/0
```

IPv6:

```text
::/0
```

---

### Q: What is a default gateway?

> A default gateway is the next-hop router used by a host to reach destinations outside its directly connected networks.

---

### Q: What is a next hop?

> A next hop is the next routing device or destination toward which a packet is forwarded.

---

### Q: What is longest prefix match?

> When multiple routes match a destination, the route with the longest, most specific prefix is generally selected.

---

### Q: What is the difference between routing and switching?

> Switching primarily forwards traffic within a local network using Layer 2 information such as MAC addresses, while routing forwards traffic between IP networks using Layer 3 information.

---

### Q: What is static routing?

> Static routing uses manually configured routes.

---

### Q: What is dynamic routing?

> Dynamic routing uses routing protocols to exchange and learn routing information.

Examples:

```text
OSPF
BGP
IS-IS
```

---

### Q: How do you view the Linux routing table?

```bash
ip route
```

---

### Q: How do you check which route Linux would use for a destination?

```bash
ip route get 8.8.8.8
```

---

### Q: How do you view IPv6 routes?

```bash
ip -6 route
```

---

### Q: How can you trace network hops?

```bash
traceroute google.com
```

---

# 🏆 What You Should Be Able to Explain

Before moving to NAT, make sure you can:

- [ ] Explain routing
- [ ] Explain forwarding
- [ ] Explain routers
- [ ] Explain routing tables
- [ ] Explain default routes
- [ ] Explain default gateways
- [ ] Explain next hops
- [ ] Explain directly connected networks
- [ ] Explain longest prefix match
- [ ] Explain static routing
- [ ] Explain dynamic routing
- [ ] Recognize OSPF
- [ ] Recognize BGP
- [ ] Explain routing vs switching
- [ ] Read a Linux routing table
- [ ] Use `ip route`
- [ ] Use `ip route get`
- [ ] Use `ip -6 route`
- [ ] Use `traceroute`
- [ ] Understand routing in AWS
- [ ] Understand routing in Docker
- [ ] Understand why routing matters in Kubernetes
- [ ] Troubleshoot a basic routing problem

---

# 🎯 Mini Project

## 🏗️ Design a Small Network

You are given:

```text
Company Network:

192.168.0.0/16
```

Design this:

```text
👨‍💻 Development
192.168.10.0/24

🧪 Testing
192.168.20.0/24

🗄️ Database
192.168.30.0/24
```

Imagine a router connects them:

```text
                    📡 Router
                  /     |      \
                 /      |       \
                ↓       ↓        ↓
         Development  Testing  Database
         10.0.10.0    10.0.20.0 10.0.30.0
```

Create a routing table:

| Destination | Next Hop | Interface |
|---|---|---|
| Development | | |
| Testing | | |
| Database | | |
| Default | | |

Then answer:

```text
1. Which networks are directly connected?
2. Which traffic needs routing?
3. What would a default route be used for?
4. Which route should win if multiple routes match?
```

---

# 🔥 DevOps Connection

Routing is one of those topics that seems boring until production breaks.

Then suddenly:

```text
🚨 "Why can't this server reach the database?"

🚨 "Why can't the private subnet access the Internet?"

🚨 "Why is my Kubernetes pod unreachable?"

🚨 "Why can't my Docker container reach the API?"

🚨 "Why is my AWS application timing out?"
```

And underneath many of these problems is some combination of:

```text
IP
Subnet
Route
Gateway
Port
Firewall
DNS
```

That's why we're learning networking **before AWS, Docker and Kubernetes**.

---

# 📚 Navigation

⬅️ Previous: **[06-Subnetting.md](06-Subnetting.md)**

➡️ Next: **[08-NAT.md](08-NAT.md)**

🏠 Networking Phase: **[README.md](README.md)**

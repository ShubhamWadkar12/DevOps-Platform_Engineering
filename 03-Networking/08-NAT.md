# 🔄 NAT (Network Address Translation)

## 🎯 What Are We Learning?

Imagine your home has:

```text
🏠 Home
│
├── 💻 Laptop
├── 📱 Phone
├── 📺 TV
└── 🖨️ Printer
```

All these devices can use private IP addresses such as:

```text
192.168.1.10
192.168.1.11
192.168.1.12
192.168.1.13
```

But the Internet doesn't directly route these private addresses.

So how does your laptop access:

```text
🌍 google.com
```

when it has:

```text
192.168.1.10
```

?

This is where **NAT** comes in.

> **NAT = Network Address Translation**

NAT translates network addresses, commonly allowing private IPv4 addresses to communicate through a public IPv4 address.

---

# 🏠 Real-Life Example

Think about an apartment building.

Inside the building:

```text
🚪 Flat 101
🚪 Flat 102
🚪 Flat 103
🚪 Flat 104
```

Everyone has their own apartment number.

But when someone outside wants to contact the building, they don't necessarily know every apartment.

They use:

```text
🏢 Building Address
```

Similarly:

```text
Private IPs
     ↓
🏠 Internal Network
     ↓
NAT
     ↓
🌍 Public IP
     ↓
Internet
```

---

# 🌐 What Is NAT?

NAT stands for:

```text
Network Address Translation
```

It changes IP addressing information as traffic passes through a NAT device.

A common home-network example:

```text
💻 Laptop
192.168.1.10
      ↓
📡 Router
      ↓
NAT
      ↓
203.0.113.50
      ↓
🌍 Internet
```

The Internet-facing traffic can use the router's public IPv4 address rather than the laptop's private address.

---

# 🤔 Why Do We Need NAT?

One major reason is **IPv4 address conservation**.

Remember:

```text
IPv4
↓
32-bit
↓
~4.3 billion addresses
```

But there are far more networked devices than that.

Private IPv4 ranges allow many different networks to reuse the same address space:

```text
Home A:
192.168.1.10

Home B:
192.168.1.10

Office C:
192.168.1.10
```

These can coexist because they're separate private networks.

NAT can then translate internal traffic to public IPv4 addresses.

---

# 🏠 Private IPv4 Reminder

The private IPv4 ranges are:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

Example:

```text
192.168.1.10
```

is private.

---

# 🌍 Simple NAT Flow

Suppose:

```text
Laptop:
192.168.1.10

Router Public IP:
203.0.113.50

Website:
198.51.100.20
```

The laptop sends traffic:

```text
192.168.1.10
        ↓
📡 Router
        ↓
NAT
        ↓
203.0.113.50
        ↓
🌍 Website
```

The NAT device maintains enough translation state to associate the return traffic with the internal connection.

---

# 🔢 NAT Table

A NAT device can maintain a translation table.

Simplified example:

| Private Source | Translated Source | Destination |
|---|---|---|
| `192.168.1.10:50001` | `203.0.113.50:40001` | `198.51.100.20:443` |
| `192.168.1.11:50002` | `203.0.113.50:40002` | `198.51.100.20:443` |

Notice something important:

Both devices can share the same public IP:

```text
203.0.113.50
```

The translation can distinguish connections using:

```text
IP addresses
+
Ports
```

This is why port numbers become important.

---

# 🚪 NAT + Ports

Suppose:

```text
Laptop A:
192.168.1.10:50001

Laptop B:
192.168.1.11:50002
```

Both connect to:

```text
google.com:443
```

The NAT device can translate them to different public source ports:

```text
Laptop A
192.168.1.10:50001
        ↓
203.0.113.50:40001

Laptop B
192.168.1.11:50002
        ↓
203.0.113.50:40002
```

So the NAT device can keep the connections separate.

---

# 🔥 PAT

You will often hear:

```text
PAT
```

PAT stands for:

```text
Port Address Translation
```

It is commonly used to allow many private IPv4 hosts to share one public IPv4 address by translating source ports.

This is often informally called:

```text
NAT Overload
```

or simply:

```text
NAT
```

in everyday networking conversations.

---

# 🆚 NAT vs PAT

| NAT | PAT |
|---|---|
| General address translation concept | Uses ports as part of translation |
| Can translate addresses | Can allow many private hosts to share one public IPv4 |
| Broader term | Specific/common technique |
| May use one-to-one mappings | Commonly many-to-one |

Think:

```text
NAT
 ↓
Change addresses

PAT
 ↓
Change addresses + ports
 ↓
Many internal devices → One public IP
```

---

# 🧩 Types of NAT

You may encounter several NAT concepts.

The most useful ones to recognize are:

```text
Static NAT
Dynamic NAT
PAT
```

---

# 1️⃣ Static NAT

Static NAT creates a fixed mapping between a private/internal address and a public/external address.

Example:

```text
192.168.1.10
       ↕
203.0.113.10
```

One internal address maps to one external address.

Think:

> 🏠 One apartment ↔ one public address

---

# 2️⃣ Dynamic NAT

Dynamic NAT maps internal addresses to addresses from a pool of public addresses.

Example:

```text
Private Network
      ↓
NAT Pool
      ↓
203.0.113.10
203.0.113.11
203.0.113.12
```

The mapping is not permanently fixed to one public address.

---

# 3️⃣ PAT

PAT allows multiple internal hosts to share a public IPv4 address using different source ports.

Example:

```text
192.168.1.10:50001
        ↓
203.0.113.50:40001

192.168.1.11:50002
        ↓
203.0.113.50:40002

192.168.1.12:50003
        ↓
203.0.113.50:40003
```

This is extremely common in home and enterprise IPv4 networks.

---

# 🏠 Your Home Wi-Fi

A typical home setup looks like:

```text
                🌍 Internet
                     │
                     │
              Public IPv4
                     │
                     ↓
              📡 Home Router
                  NAT/PAT
                     │
             ┌───────┼───────┐
             ↓       ↓       ↓
            💻      📱      📺
        192.168.1.x
```

Your devices use private IP addresses.

The router translates their traffic when communicating with the public Internet.

---

# 🔄 What Happens When You Open a Website?

You type:

```text
https://example.com
```

A simplified flow is:

```text
1️⃣ Browser creates HTTPS traffic

        ↓

2️⃣ Device creates an outbound connection

        ↓

3️⃣ Packet reaches the router

        ↓

4️⃣ Router performs NAT/PAT

        ↓

5️⃣ Traffic goes to the Internet

        ↓

6️⃣ Website responds

        ↓

7️⃣ NAT device uses its translation state

        ↓

8️⃣ Response is forwarded to the correct internal device
```

---

# 📦 Visual Example

```text
💻 Laptop
192.168.1.10:50001
       │
       │
       ↓
📡 Router
       │
       │ NAT/PAT
       ↓
203.0.113.50:40001
       │
       ↓
🌍 Internet
       │
       ↓
🖥️ Web Server
198.51.100.20:443
```

Return traffic:

```text
🖥️ Web Server
      ↓
203.0.113.50:40001
      ↓
📡 NAT Router
      ↓
192.168.1.10:50001
      ↓
💻 Laptop
```

---

# 🚨 Important: NAT Is Not the Same as a Firewall

This is a common misconception.

NAT:

> Changes or translates addressing information.

Firewall:

> Controls whether traffic is allowed or denied according to security rules.

A home router may perform both:

```text
📡 Router
│
├── NAT/PAT
│
└── Firewall
```

But they are different functions.

---

# 🔐 Does NAT Provide Security?

NAT can make internal addressing less directly exposed to the public Internet.

However:

> **NAT is not a security boundary by itself.**

Security should be provided by mechanisms such as:

```text
Firewalls
Security Groups
Network ACLs
Application Security
Authentication
Encryption
```

So don't say in an interview:

> "NAT is a firewall."

❌ Wrong.

Better:

> "NAT performs address translation; firewall policies control whether traffic is allowed."

---

# 🌐 Inbound Connections

Here's an interesting question.

Suppose your laptop is:

```text
192.168.1.10
```

That's a private IP.

Someone on the Internet tries:

```text
🌍 Internet
    ↓
192.168.1.10
```

That won't work as a normal Internet-routed destination.

Private addresses are not globally routable.

If you want an Internet user to reach an internal service, you need appropriate mechanisms such as:

```text
Public IP
+
NAT / Port Forwarding
+
Firewall Rules
```

---

# 🚪 Port Forwarding

Port forwarding is a common form of destination NAT.

Example:

```text
🌍 Internet
203.0.113.50:8080
        ↓
📡 Router
        ↓
192.168.1.10:80
        ↓
🖥️ Web Server
```

The router receives traffic on:

```text
Public IP : 8080
```

and forwards it to:

```text
Private IP : 80
```

---

# 🏠 Real-Life Example

Imagine:

```text
🏢 Building
Public Address:
203.0.113.50
```

Someone says:

> "Deliver this to apartment 101."

The building receptionist knows:

```text
External Door 8080
        ↓
Apartment 101
```

That's similar to port forwarding.

---

# ☁️ NAT in AWS

NAT becomes very important in AWS.

Imagine:

```text
☁️ AWS VPC
│
├── 🌐 Public Subnet
│
└── 🔒 Private Subnet
        │
        └── 🖥️ EC2
```

Suppose the private EC2 needs to download:

```text
OS updates
Packages
Container images
```

But you don't want the EC2 instance to have a directly reachable public IPv4 address.

A common architecture is:

```text
Private EC2
    ↓
Route Table
    ↓
NAT Gateway
    ↓
Internet Gateway
    ↓
🌍 Internet
```

The private instance can initiate outbound connections through the NAT Gateway.

---

# ☁️ AWS NAT Gateway

A common AWS architecture:

```text
                    🌍 Internet
                         │
                         ↓
                🌐 Internet Gateway
                         │
                         ↓
                  🟢 Public Subnet
                         │
                    NAT Gateway
                         │
                         ↓
                  🔒 Private Subnet
                         │
                      🖥️ EC2
```

The private instance doesn't need a public IPv4 address simply to make outbound Internet connections through this architecture.

---

# 🔐 Why Use a Private Subnet?

Imagine your application server:

```text
🖥️ Application Server
```

You may not want it directly exposed to the Internet.

Instead:

```text
🌍 Internet
      ↓
⚖️ Load Balancer
      ↓
🔒 Private Application Subnet
      ↓
🗄️ Database
```

For outbound access:

```text
Private Server
      ↓
NAT Gateway
      ↓
Internet
```

This is a common cloud architecture pattern.

---

# 🧠 Important AWS Difference

A NAT Gateway is primarily for:

```text
Private Subnet
      ↓
Outbound Internet
```

It is not a general mechanism for allowing unsolicited inbound Internet traffic to private instances.

Remember:

```text
Private EC2
     ↓
NAT Gateway
     ↓
Internet
```

Not:

```text
Internet
     ↓
NAT Gateway
     ↓
Private EC2
```

for arbitrary inbound connections.

---

# 🐳 NAT + Docker

Docker commonly uses NAT for container connectivity.

A simplified setup:

```text
🌍 Internet
     ↓
Host
     ↓
Docker NAT
     ↓
Container
```

Suppose:

```text
Container:
172.17.0.2:80

Host:
8080
```

You can publish:

```text
Host Port 8080
      ↓
Container Port 80
```

Example:

```bash
docker run -p 8080:80 nginx
```

Then:

```text
Browser
   ↓
localhost:8080
   ↓
Docker
   ↓
Container:80
```

Docker networking has additional details, but NAT/port translation is an important part of understanding how published ports work.

---

# ☸️ NAT + Kubernetes

Kubernetes networking can also involve NAT depending on the network path and CNI configuration.

For example, pod traffic may leave the cluster through a node and be translated before reaching an external network.

Conceptually:

```text
Pod
 ↓
Node
 ↓
NAT
 ↓
External Network
```

The exact behavior depends on:

```text
CNI
Cluster configuration
Cloud provider
Routing
Network policies
```

Don't assume every Kubernetes cluster uses exactly the same NAT behavior.

---

# 🔥 SNAT

SNAT stands for:

```text
Source Network Address Translation
```

It changes the **source address** of traffic.

Example:

```text
Before:

192.168.1.10
     ↓
Internet


After:

203.0.113.50
     ↓
Internet
```

The source address was translated.

Think:

> **SNAT = change where the traffic appears to come from.**

---

# 🔥 DNAT

DNAT stands for:

```text
Destination Network Address Translation
```

It changes the **destination address** of traffic.

Example:

```text
Before:

203.0.113.50:8080
        ↓

After:

192.168.1.10:80
```

Think:

> **DNAT = change where the traffic is going.**

---

# 🆚 SNAT vs DNAT

| Type | Changes | Common Example |
|---|---|---|
| SNAT | Source | Private host → Internet |
| DNAT | Destination | Port forwarding |
| PAT | Address + Port translation | Many hosts → One public IP |

Remember:

```text
SNAT
Source changes

DNAT
Destination changes
```

---

# 🧠 NAT Terminology

You'll encounter these terms:

```text
Inside Local
Inside Global
Outside Local
Outside Global
```

These are especially common in traditional networking discussions.

For DevOps interviews, first make sure you're comfortable with:

```text
Private IP
Public IP
NAT
PAT
SNAT
DNAT
Port Forwarding
NAT Gateway
```

Then learn the more detailed terminology when needed.

---

# 🧪 Linux NAT Investigation

On Linux, NAT is commonly implemented using:

```text
Netfilter
iptables
nftables
```

Modern Linux systems increasingly use:

```text
nftables
```

while `iptables` remains very common in existing systems and documentation.

You may encounter commands such as:

```bash
sudo nft list ruleset
```

or:

```bash
sudo iptables -t nat -L -n -v
```

⚠️ Don't modify firewall/NAT rules on your main WSL environment unless you know how to restore them.

For now, **inspection is enough**.

---

# 🧪 Hands-on Lab

## Mission 1 — Check Your IP

Run:

```bash
ip addr
```

Find your private IPv4 address.

Example:

```text
192.168.x.x
```

or:

```text
172.x.x.x
```

or:

```text
10.x.x.x
```

---

## Mission 2 — Check Your Default Gateway

Run:

```bash
ip route
```

Find:

```text
default via X.X.X.X
```

---

## Mission 3 — Understand the Path

Run:

```bash
ip route get 8.8.8.8
```

Look for:

```text
via
dev
src
```

Try to identify:

```text
Destination:
Next Hop:
Interface:
Source IP:
```

---

## Mission 4 — Check NAT Rules

If your environment allows it, try:

```bash
sudo nft list ruleset
```

If `nft` isn't available, don't install anything just for this exercise.

You can also check:

```bash
sudo iptables -t nat -L -n -v
```

Again, we're inspecting, not modifying.

---

# 🎮 Real-Life Troubleshooting Challenge

Your application is running inside a private subnet:

```text
🖥️ EC2
10.0.2.10
```

It needs to download packages from the Internet.

But:

```text
curl https://example.com
```

fails.

You investigate:

```text
EC2
 ↓
Route Table
 ↓
NAT Gateway
 ↓
Internet Gateway
 ↓
Internet
```

Check:

```text
1️⃣ Does the subnet route Internet traffic to the NAT Gateway?

2️⃣ Is the NAT Gateway in a public subnet?

3️⃣ Does the public subnet have a route to an Internet Gateway?

4️⃣ Does the private subnet have the correct route?

5️⃣ Are security rules allowing the traffic?

6️⃣ Is DNS working?
```

This is exactly the kind of troubleshooting you'll do later in AWS.

---

# 🎮 Mini Challenge

Consider:

```text
Laptop A:
192.168.1.10:50001

Laptop B:
192.168.1.11:50002

Public IP:
203.0.113.50
```

Both access:

```text
198.51.100.20:443
```

The NAT device creates:

```text
192.168.1.10:50001
        ↓
203.0.113.50:40001
```

and:

```text
192.168.1.11:50002
        ↓
203.0.113.50:40002
```

### Question:

How can both laptops use the same public IP?

### Answer:

The NAT/PAT device uses different translated source ports to keep the connections distinguishable.

---

# 🧠 NAT Flow to Remember

For normal outbound IPv4 traffic:

```text
Private Host
     ↓
Private IP
     ↓
NAT/PAT Device
     ↓
Public IP + Translated Port
     ↓
Internet
```

Return:

```text
Internet
     ↓
Public IP + Translated Port
     ↓
NAT/PAT Device
     ↓
Private IP + Original Port
     ↓
Private Host
```

---

# 🚨 Common Misconceptions

## ❌ "NAT gives a private IP Internet access by itself."

Not necessarily.

You also need appropriate:

```text
Routing
NAT configuration
Firewall/security rules
Upstream connectivity
```

---

## ❌ "NAT is a firewall."

No.

```text
NAT
→ Address translation

Firewall
→ Traffic control
```

---

## ❌ "NAT is required for IPv6."

No.

IPv6 was designed with a vastly larger address space, so NAT is not required to solve IPv4 address exhaustion.

---

## ❌ "Private IPs are always secure."

No.

Private addressing doesn't automatically make an application secure.

Security depends on:

```text
Firewall rules
Network segmentation
Authentication
Encryption
Application security
```

---

# 💼 Interview Corner

### Q: What is NAT?

> NAT, or Network Address Translation, translates IP addresses as traffic passes between networks, commonly allowing private IPv4 hosts to communicate using public IPv4 addresses.

---

### Q: Why is NAT commonly used?

> NAT is commonly used to conserve public IPv4 addresses and allow private IPv4 networks to communicate with external networks.

---

### Q: What is PAT?

> PAT is a form of address translation that uses transport-layer ports to allow multiple internal hosts to share a public IPv4 address.

---

### Q: What is SNAT?

> SNAT changes the source address of a packet, commonly allowing private hosts to appear to originate from a public address.

---

### Q: What is DNAT?

> DNAT changes the destination address of a packet and is commonly used for port forwarding.

---

### Q: What is port forwarding?

> Port forwarding maps traffic arriving at a public address and port to an internal address and port.

---

### Q: Is NAT a firewall?

> No. NAT performs address translation, while a firewall enforces traffic-control policies.

---

### Q: What is an AWS NAT Gateway used for?

> An AWS NAT Gateway is commonly used to allow resources in private subnets to initiate outbound connections to the Internet without assigning public IPv4 addresses to those resources.

---

### Q: Does NAT eliminate the need for firewalls?

```text
No ❌
```

NAT and firewalling solve different problems.

---

### Q: What is the difference between SNAT and DNAT?

```text
SNAT → Source changes
DNAT → Destination changes
```

---

# 🏆 What You Should Be Able to Explain

Before moving to protocols, make sure you can:

- [ ] Explain NAT
- [ ] Explain why NAT is used
- [ ] Explain private vs public IPv4
- [ ] Explain NAT/PAT
- [ ] Explain Static NAT
- [ ] Explain Dynamic NAT
- [ ] Explain PAT
- [ ] Explain SNAT
- [ ] Explain DNAT
- [ ] Explain port forwarding
- [ ] Explain NAT vs firewall
- [ ] Explain NAT and ports
- [ ] Explain outbound NAT
- [ ] Explain how return traffic is translated
- [ ] Explain NAT in home networks
- [ ] Explain NAT in AWS
- [ ] Explain NAT in Docker
- [ ] Understand where NAT may appear in Kubernetes networking
- [ ] Recognize Linux NAT tooling
- [ ] Troubleshoot a basic NAT connectivity problem

---

# 🎯 Mini Project

## 🏠 Design a Home Network

Design this:

```text
                    🌍 Internet
                         │
                         │
                   Public IP
                         │
                         ↓
                    📡 Router
                    NAT/PAT
                         │
              ┌──────────┼──────────┐
              ↓          ↓          ↓
             💻         📱         📺
          Laptop       Phone        TV
```

Use:

```text
Public IP:
203.0.113.50

Laptop:
192.168.1.10

Phone:
192.168.1.11

TV:
192.168.1.12
```

Create a NAT table:

| Internal Device | Private IP:Port | Public IP:Port |
|---|---|---|
| Laptop | | |
| Phone | | |
| TV | | |

Choose your own example source ports.

Then explain:

```text
1. Why can all three devices share one public IP?

2. Why are their private IPs not Internet-routable?

3. What role does the router play?

4. What role does NAT/PAT play?

5. What would happen to return traffic?

6. Why is NAT not a replacement for a firewall?
```

---

# 🔥 DevOps Connection

NAT might look like an old networking topic.

It isn't.

You'll see it again and again:

```text
🏠 Home Networks
      ↓
NAT/PAT

🐳 Docker
      ↓
Container Networking

☁️ AWS
      ↓
NAT Gateway

☸️ Kubernetes
      ↓
Cluster/Node Networking

🏢 Enterprise
      ↓
Private Networks
```

When production says:

> 🚨 "The private server can reach some services but not the Internet."

you'll start thinking:

```text
IP
 ↓
Subnet
 ↓
Route
 ↓
NAT
 ↓
Firewall
 ↓
DNS
 ↓
Application
```

That's the networking mindset we're building. 🔥

---

# 📚 Navigation

⬅️ Previous: **[07-Routing.md](07-Routing.md)**

➡️ Next: **[09-Protocols.md](09-Protocols.md)**

🏠 Networking Phase: **[README.md](README.md)**

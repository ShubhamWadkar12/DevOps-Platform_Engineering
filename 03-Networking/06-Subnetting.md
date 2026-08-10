# 🧩 Subnetting

## 🎯 What Are We Learning?

Imagine your college has **1,000 students**.

You could put everyone into one giant classroom:

```text
🏫 College Network
│
├── 👨‍🎓 Student
├── 👨‍🎓 Student
├── 👨‍🎓 Student
├── ...
└── 👨‍🎓 1000 Students
```

But that's messy.

Instead, you divide them into smaller classrooms:

```text
🏫 College
│
├── 🏫 Classroom A → 250 students
├── 🏫 Classroom B → 250 students
├── 🏫 Classroom C → 250 students
└── 🏫 Classroom D → 250 students
```

That's basically the idea behind **subnetting**.

> **Subnetting = dividing one larger IP network into smaller networks.**

---

# 🌐 Why Do We Need Subnetting?

Imagine a company has:

```text
10.0.0.0/16
```

That's a large network.

Instead of putting everything together:

```text
💻 Developers
🗄️ Databases
🔐 Security
🖥️ Servers
📡 Network Devices
```

we can divide the network:

```text
10.0.0.0/16
      │
      ├── 10.0.1.0/24  → Developers
      ├── 10.0.2.0/24  → Applications
      ├── 10.0.3.0/24  → Databases
      └── 10.0.4.0/24  → Infrastructure
```

Now we have smaller, organized networks.

---

# 🧠 What Exactly Is a Subnet?

A subnet is a logical subdivision of an IP network.

For example:

```text
192.168.1.0/24
```

can be considered one subnet.

Inside it:

```text
Network:
192.168.1.0

Hosts:
192.168.1.1
192.168.1.2
...
192.168.1.254

Broadcast:
192.168.1.255
```

---

# 🏠 Real-Life Analogy

Think about an apartment complex.

```text
🏢 Apartment Complex
       ↓
     Network
       ↓
┌──────┬──────┬──────┬──────┐
│ Flat │ Flat │ Flat │ Flat │
└──────┴──────┴──────┴──────┘
       ↓
      Hosts
```

The apartment complex is the:

```text
Network
```

Each apartment is a:

```text
Host
```

Subnetting lets us divide a large complex into smaller sections.

---

# 🔢 IPv4 Review

Before subnetting, remember:

IPv4 uses:

```text
32 bits
```

Example:

```text
192.168.1.10
```

Binary:

```text
11000000.10101000.00000001.00001010
```

Each octet:

```text
8 bits
```

Therefore:

```text
8 + 8 + 8 + 8 = 32 bits
```

---

# 🧩 Network Bits vs Host Bits

An IPv4 address contains:

```text
Network Portion
+
Host Portion
```

For:

```text
192.168.1.10/24
```

we have:

```text
Network bits = 24
Host bits    = 8
```

Visual:

```text
192.168.1.10
└─────────┘ └┘
 Network   Host
   24       8
```

---

# 🔢 What Does `/24` Mean?

This:

```text
192.168.1.10/24
```

means:

```text
First 24 bits → Network Prefix
Remaining 8 bits → Host Portion
```

Since 8 bits remain for hosts:

```text
2⁸ = 256
```

So the subnet contains:

```text
256 total addresses
```

For a traditional IPv4 `/24` subnet:

```text
1 Network Address
254 Usable Host Addresses
1 Broadcast Address
```

---

# 🧮 The Basic Formula

For IPv4:

```text
Total Addresses = 2^(Host Bits)
```

Traditional usable host count:

```text
Usable Hosts = 2^(Host Bits) - 2
```

Why subtract 2?

Because traditionally:

```text
First address → Network Address
Last address  → Broadcast Address
```

---

# 🎮 Mini Challenge

For:

```text
192.168.1.0/24
```

How many host bits?

```text
32 - 24 = 8
```

Total addresses:

```text
2⁸ = 256
```

Traditional usable hosts:

```text
256 - 2 = 254
```

Therefore:

```text
Network:
192.168.1.0

Usable:
192.168.1.1
-
192.168.1.254

Broadcast:
192.168.1.255
```

---

# 🧱 Subnet Masks

CIDR notation:

```text
/24
```

has a corresponding subnet mask:

```text
255.255.255.0
```

Some common examples:

| CIDR | Subnet Mask |
|---|---|
| `/8` | `255.0.0.0` |
| `/16` | `255.255.0.0` |
| `/24` | `255.255.255.0` |
| `/25` | `255.255.255.128` |
| `/26` | `255.255.255.192` |
| `/27` | `255.255.255.224` |
| `/28` | `255.255.255.240` |
| `/29` | `255.255.255.248` |
| `/30` | `255.255.255.252` |

You don't need to blindly memorize all of them.

We'll learn how to calculate them.

---

# 🧮 The Magic Numbers

When subnetting, these values appear constantly:

```text
128
64
32
16
8
4
2
1
```

They come from:

```text
2⁷ = 128
2⁶ = 64
2⁵ = 32
2⁴ = 16
2³ = 8
2² = 4
2¹ = 2
2⁰ = 1
```

You'll use these to calculate subnet masks and subnet ranges.

---

# 🧩 Borrowing Bits

Here's where subnetting gets interesting.

Suppose we have:

```text
192.168.1.0/24
```

We want **2 smaller networks**.

We need to borrow one host bit.

Original:

```text
/24
```

After borrowing one bit:

```text
/25
```

So:

```text
/24
    ↓
/25
```

---

# 🔢 Why Does `/25` Give 2 Subnets?

A single bit has:

```text
0
1
```

Two possible values.

Therefore:

```text
2¹ = 2 subnets
```

So:

```text
192.168.1.0/24
```

can be divided into:

```text
192.168.1.0/25
192.168.1.128/25
```

---

# 🏠 Visualize It

Original:

```text
192.168.1.0/24

┌────────────────────────────────────┐
│          256 addresses             │
└────────────────────────────────────┘
```

After subnetting:

```text
192.168.1.0/25
┌──────────────────┐
│ 128 addresses    │
└──────────────────┘

192.168.1.128/25
┌──────────────────┐
│ 128 addresses    │
└──────────────────┘
```

---

# 🧮 `/25` Breakdown

For:

```text
192.168.1.0/25
```

Host bits:

```text
32 - 25 = 7
```

Total addresses:

```text
2⁷ = 128
```

Traditional usable hosts:

```text
128 - 2 = 126
```

First subnet:

```text
Network:
192.168.1.0

Usable:
192.168.1.1
-
192.168.1.126

Broadcast:
192.168.1.127
```

Second subnet:

```text
Network:
192.168.1.128

Usable:
192.168.1.129
-
192.168.1.254

Broadcast:
192.168.1.255
```

---

# 🎮 Mini Challenge

Divide:

```text
192.168.10.0/24
```

into two `/25` networks.

### Answer

```text
Subnet 1:
192.168.10.0/25

Subnet 2:
192.168.10.128/25
```

---

# 🧩 Creating 4 Subnets

Suppose we start with:

```text
192.168.1.0/24
```

We want:

```text
4 subnets
```

How many bits do we need?

```text
2² = 4
```

So borrow:

```text
2 bits
```

New prefix:

```text
/24 + 2 = /26
```

Therefore:

```text
192.168.1.0/26
```

---

# 🔢 `/26` Breakdown

Host bits:

```text
32 - 26 = 6
```

Total addresses:

```text
2⁶ = 64
```

Traditional usable:

```text
64 - 2 = 62
```

So each `/26` subnet has:

```text
64 total addresses
62 traditional usable host addresses
```

---

# 🧩 The Four `/26` Networks

Starting network:

```text
192.168.1.0/24
```

Divide into `/26`:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

# 📦 Full Breakdown

## Subnet 1

```text
Network:
192.168.1.0

Usable:
192.168.1.1
-
192.168.1.62

Broadcast:
192.168.1.63
```

## Subnet 2

```text
Network:
192.168.1.64

Usable:
192.168.1.65
-
192.168.1.126

Broadcast:
192.168.1.127
```

## Subnet 3

```text
Network:
192.168.1.128

Usable:
192.168.1.129
-
192.168.1.190

Broadcast:
192.168.1.191
```

## Subnet 4

```text
Network:
192.168.1.192

Usable:
192.168.1.193
-
192.168.1.254

Broadcast:
192.168.1.255
```

---

# 🧠 The Subnetting Pattern

Notice something?

For `/26`:

```text
Block Size = 64
```

So the networks start at:

```text
0
64
128
192
```

This is extremely useful.

---

# 🧮 Block Size

A quick formula:

```text
Block Size = 256 - Subnet Mask Value
```

For `/26`:

```text
Subnet Mask:

255.255.255.192
```

Therefore:

```text
256 - 192 = 64
```

Block size:

```text
64
```

Networks:

```text
0
64
128
192
```

---

# 🔢 Common Subnet Masks

| CIDR | Mask | Block Size |
|---|---|---:|
| `/24` | `255.255.255.0` | 256 |
| `/25` | `255.255.255.128` | 128 |
| `/26` | `255.255.255.192` | 64 |
| `/27` | `255.255.255.224` | 32 |
| `/28` | `255.255.255.240` | 16 |
| `/29` | `255.255.255.248` | 8 |
| `/30` | `255.255.255.252` | 4 |

---

# 🧮 `/27`

Let's calculate.

```text
32 - 27 = 5 host bits
```

Total:

```text
2⁵ = 32
```

Traditional usable:

```text
32 - 2 = 30
```

Subnet mask:

```text
255.255.255.224
```

Block size:

```text
256 - 224 = 32
```

So:

```text
192.168.1.0/27
192.168.1.32/27
192.168.1.64/27
192.168.1.96/27
192.168.1.128/27
192.168.1.160/27
192.168.1.192/27
192.168.1.224/27
```

That's:

```text
8 subnets
```

---

# 🧮 `/28`

Host bits:

```text
32 - 28 = 4
```

Total:

```text
2⁴ = 16
```

Traditional usable:

```text
16 - 2 = 14
```

Mask:

```text
255.255.255.240
```

Block size:

```text
256 - 240 = 16
```

Networks:

```text
192.168.1.0/28
192.168.1.16/28
192.168.1.32/28
192.168.1.48/28
192.168.1.64/28
192.168.1.80/28
192.168.1.96/28
192.168.1.112/28
192.168.1.128/28
192.168.1.144/28
192.168.1.160/28
192.168.1.176/28
192.168.1.192/28
192.168.1.208/28
192.168.1.224/28
192.168.1.240/28
```

---

# 🚪 `/30`

A `/30` subnet has:

```text
32 - 30 = 2 host bits
```

Total:

```text
2² = 4 addresses
```

Traditional usable:

```text
4 - 2 = 2
```

Example:

```text
10.0.0.0/30
```

```text
Network:
10.0.0.0

Host:
10.0.0.1
10.0.0.2

Broadcast:
10.0.0.3
```

This historically became common for point-to-point IPv4 links.

---

# 🏠 Real-Life Example

Imagine you have:

```text
🏢 Company
100 employees
```

You have:

```text
10.0.0.0/24
```

But you want:

```text
👨‍💻 Development → 50 hosts
🧪 Testing      → 50 hosts
🗄️ Database     → 50 hosts
🔐 Security     → 50 hosts
```

You can divide the `/24` into four `/26` networks:

```text
10.0.0.0/26
      ↓
Development

10.0.0.64/26
      ↓
Testing

10.0.0.128/26
      ↓
Database

10.0.0.192/26
      ↓
Security
```

Each subnet has:

```text
64 total addresses
62 traditional usable host addresses
```

Perfect fit.

---

# ☁️ Subnetting in AWS

Now subnetting becomes **very important**.

Imagine an AWS VPC:

```text
☁️ VPC
10.0.0.0/16
```

You can create smaller subnets:

```text
10.0.1.0/24 → Public Subnet
10.0.2.0/24 → Private Subnet
10.0.3.0/24 → Database Subnet
```

For example:

```text
                 ☁️ VPC
              10.0.0.0/16
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
  Public         Private      Database
 10.0.1.0/24    10.0.2.0/24   10.0.3.0/24
```

This is one of the most important networking concepts you'll use in AWS.

---

# ☸️ Subnetting + Kubernetes

Kubernetes also uses network ranges.

You may eventually encounter:

```text
Pod CIDR
Service CIDR
Node Network
```

Example:

```text
Cluster
│
├── Node 1
│    ├── Pod
│    └── Pod
│
├── Node 2
│    ├── Pod
│    └── Pod
```

The underlying networking depends on the Kubernetes CNI and cluster configuration.

Subnetting knowledge will make those concepts much easier.

---

# 🐳 Subnetting + Docker

Docker networks also use IP ranges.

Example:

```text
Docker Network
172.18.0.0/16
       │
       ├── Container A
       ├── Container B
       └── Container C
```

The Docker network provides an IP space from which containers can receive addresses.

---

# 🧮 Finding Which Subnet an IP Belongs To

This is a very important skill.

Suppose:

```text
IP:
192.168.1.70/26
```

We know `/26` has:

```text
Block Size = 64
```

Network boundaries:

```text
0
64
128
192
```

Where does `70` fall?

```text
64 ≤ 70 < 128
```

Therefore:

```text
Network:
192.168.1.64/26
```

Broadcast:

```text
192.168.1.127
```

Usable:

```text
192.168.1.65
-
192.168.1.126
```

---

# 🎮 Mini Challenge

Find the subnet for:

```text
192.168.10.130/26
```

Block size:

```text
64
```

Network boundaries:

```text
0
64
128
192
```

`130` falls between:

```text
128
-
191
```

Therefore:

```text
Network:
192.168.10.128/26

Broadcast:
192.168.10.191

Usable:
192.168.10.129
-
192.168.10.190
```

---

# 🎮 Mini Challenge 2

Find the subnet for:

```text
10.10.10.45/27
```

For `/27`:

```text
Block Size = 32
```

Boundaries:

```text
0
32
64
96
...
```

`45` falls between:

```text
32
-
63
```

Therefore:

```text
Network:
10.10.10.32/27

Broadcast:
10.10.10.63

Usable:
10.10.10.33
-
10.10.10.62
```

---

# 🎯 Same Subnet or Different?

This is another common interview question.

Suppose:

```text
A = 192.168.1.10/24
B = 192.168.1.50/24
```

Both belong to:

```text
192.168.1.0/24
```

Therefore:

```text
Same subnet ✅
```

Now:

```text
A = 192.168.1.10/24
B = 192.168.2.10/24
```

Networks:

```text
A → 192.168.1.0/24
B → 192.168.2.0/24
```

Therefore:

```text
Different subnet ❌
```

---

# 🧠 Why Does Same Subnet Matter?

Suppose:

```text
💻 A
192.168.1.10

💻 B
192.168.1.20
```

If they're in the same subnet, they can generally communicate directly at Layer 2, subject to local network configuration and security controls.

But if:

```text
💻 A
192.168.1.10

💻 B
192.168.2.20
```

they're in different IP networks.

Traffic generally needs a router or Layer 3 forwarding device.

Think:

```text
Same classroom
     ↓
Talk directly

Different classroom
     ↓
Go through the corridor/door/router
```

---

# 🚨 Real DevOps Scenario

Your AWS application has:

```text
Web Server:
10.0.1.10/24

Database:
10.0.2.10/24
```

A developer says:

> "The application cannot connect to the database."

Don't immediately assume the database is broken.

Ask:

```text
Are they in the same subnet?
        ↓
No
        ↓
Is routing configured?
        ↓
Are security rules allowing the traffic?
        ↓
Is the database listening?
        ↓
Is DNS correct?
```

Subnetting helps you understand the first question immediately.

---

# 🔥 VLSM — Variable Length Subnet Masking

Real networks don't always need equal-sized subnets.

Suppose:

```text
Development → 100 hosts
Testing     → 30 hosts
Database    → 10 hosts
```

Giving everyone `/25` would waste addresses.

Instead, we can use different subnet sizes.

For example:

```text
Development → /25
Testing     → /27
Database    → /28
```

This is called:

```text
VLSM
Variable Length Subnet Masking
```

The idea:

> **Give each network the size it actually needs.**

This becomes useful in real infrastructure design.

---

# 🧠 Subnetting Cheat Sheet

```text
CIDR      Host Bits     Total Addresses
/24          8                256
/25          7                128
/26          6                 64
/27          5                 32
/28          4                 16
/29          3                  8
/30          2                  4
```

Traditional IPv4 usable hosts:

```text
/24 → 254
/25 → 126
/26 → 62
/27 → 30
/28 → 14
/29 → 6
/30 → 2
```

> ⚠️ The traditional "subtract 2" rule is for conventional IPv4 subnets where the network and broadcast addresses are reserved. Some environments have special rules, so always check the platform's documentation.

---

# 🧪 Hands-on Linux

Linux can help you inspect network addresses and prefixes.

Run:

```bash
ip addr
```

Look for something like:

```text
inet 192.168.1.10/24
```

The:

```text
/24
```

is your prefix length.

You can also inspect routes:

```bash
ip route
```

Example:

```text
192.168.1.0/24 dev eth0
```

This tells you that the interface has a route for:

```text
192.168.1.0/24
```

---

# 🎮 Subnetting Mission

Solve these **without looking at the answers first**.

---

## Challenge 1

```text
192.168.1.10/24
```

Find:

```text
Network:
Broadcast:
Usable Range:
Total Addresses:
```

---

## Challenge 2

```text
192.168.1.70/26
```

Find:

```text
Network:
Broadcast:
Usable Range:
```

---

## Challenge 3

```text
10.0.0.130/25
```

Find:

```text
Network:
Broadcast:
Usable Range:
```

---

## Challenge 4

```text
172.16.10.35/27
```

Find:

```text
Network:
Broadcast:
Usable Range:
```

---

# ✅ Answers

## Challenge 1

```text
IP:
192.168.1.10/24

Network:
192.168.1.0

Broadcast:
192.168.1.255

Usable:
192.168.1.1
-
192.168.1.254

Total:
256
```

---

## Challenge 2

```text
IP:
192.168.1.70/26

Network:
192.168.1.64

Broadcast:
192.168.1.127

Usable:
192.168.1.65
-
192.168.1.126
```

---

## Challenge 3

```text
IP:
10.0.0.130/25

Network:
10.0.0.128

Broadcast:
10.0.0.255

Usable:
10.0.0.129
-
10.0.0.254
```

---

## Challenge 4

```text
IP:
172.16.10.35/27

Network:
172.16.10.32

Broadcast:
172.16.10.63

Usable:
172.16.10.33
-
172.16.10.62
```

---

# 💼 Interview Corner

### Q: What is subnetting?

> Subnetting is the process of dividing a larger IP network into smaller logical networks called subnets.

---

### Q: Why do we use subnetting?

> Subnetting helps organize networks, control address allocation, reduce unnecessary broadcast domains, and apply network segmentation.

---

### Q: What does `/24` mean?

> `/24` means the first 24 bits are the network prefix and the remaining 8 bits are available for the host portion.

---

### Q: How many addresses are in a `/24`?

```text
2⁸ = 256
```

---

### Q: How many traditional usable hosts are in a `/24`?

```text
254
```

---

### Q: How many subnets can you create by borrowing 2 bits?

```text
2² = 4
```

---

### Q: What is the subnet mask for `/26`?

```text
255.255.255.192
```

---

### Q: What is the block size of `/26`?

```text
256 - 192 = 64
```

---

### Q: What is VLSM?

> VLSM allows different subnet sizes to be used within a network so address space can be allocated more efficiently.

---

### Q: Two machines are in different subnets. Can they communicate?

> Yes, but communication between different IP networks generally requires Layer 3 routing, along with appropriate routing and security configuration.

---

### Q: Why is subnetting important for DevOps?

> Because cloud VPCs, Kubernetes networking, Docker networks, routing, security boundaries, and production infrastructure all rely heavily on IP addressing and subnet design.

---

# 🧠 The Subnetting Method

When you see:

```text
192.168.10.70/26
```

Don't panic.

Follow this process:

```text
STEP 1
Find host bits

32 - 26 = 6

        ↓

STEP 2
Find total addresses

2⁶ = 64

        ↓

STEP 3
Find block size

64

        ↓

STEP 4
Find network boundaries

0
64
128
192

        ↓

STEP 5
Find where 70 falls

64 ≤ 70 < 128

        ↓

STEP 6
Network = 64

        ↓

STEP 7
Broadcast = 127

        ↓

STEP 8
Usable = 65 - 126
```

That's your subnetting workflow. 🔥

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain subnetting
- [ ] Explain why subnetting is needed
- [ ] Explain network vs host bits
- [ ] Explain CIDR
- [ ] Calculate host bits
- [ ] Calculate total addresses
- [ ] Calculate traditional usable hosts
- [ ] Convert common CIDR prefixes to subnet masks
- [ ] Calculate block size
- [ ] Find network addresses
- [ ] Find broadcast addresses
- [ ] Find usable host ranges
- [ ] Determine whether two IPs belong to the same subnet
- [ ] Divide `/24` into `/25`
- [ ] Divide `/24` into `/26`
- [ ] Divide `/24` into `/27`
- [ ] Understand `/28`, `/29`, `/30`
- [ ] Understand VLSM
- [ ] Understand subnetting in AWS
- [ ] Understand subnetting in Docker
- [ ] Understand why subnetting matters in Kubernetes
- [ ] Troubleshoot basic subnet-related problems

---

# 🎯 Mini Project

## 🏗️ Design a Small Company Network

You are given:

```text
Company Network:

10.10.0.0/24
```

You need:

```text
👨‍💻 Development → 60 hosts
🧪 Testing      → 30 hosts
🗄️ Database     → 30 hosts
🔐 Management   → 10 hosts
```

### Your task

Design the subnets.

Try to use the smallest suitable subnet for each department.

Create a table:

| Department | Network | CIDR | Usable Range | Broadcast |
|---|---|---|---|---|
| Development | | | | |
| Testing | | | | |
| Database | | | | |
| Management | | | | |

### 💡 Hint

Think:

```text
60 hosts → ?
30 hosts → ?
30 hosts → ?
10 hosts → ?
```

Don't look for the answer immediately.

**Try calculating it yourself.**

This is exactly the kind of thinking you'll later use when designing:

```text
☁️ AWS VPCs
☸️ Kubernetes Networks
🐳 Docker Networks
🏢 Enterprise Infrastructure
```

---

# 📚 Navigation

⬅️ Previous: **[05-IPv6.md](05-IPv6.md)**

➡️ Next: **[07-Routing.md](07-Routing.md)**

🏠 Networking Phase: **[README.md](README.md)**

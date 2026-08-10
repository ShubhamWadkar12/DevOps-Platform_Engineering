# 🔗 VPC Peering

## 🎯 What Are We Learning?

Imagine two offices:

```text
🏢 Company Office A

🏢 Company Office B
```

Both offices have their own private networks.

They need to communicate:

```text
Office A
   │
   │ 🔗 Private Connection
   │
Office B
```

In AWS, two VPCs can be connected using:

> **VPC Peering**

VPC Peering allows resources in two VPCs to communicate using private IP addresses, subject to routing and security rules.

---

# 🧠 What Is VPC Peering?

VPC Peering is a networking connection between two VPCs.

Example:

```text
☁️ VPC A
10.0.0.0/16

        🔗
    VPC Peering
        🔗

☁️ VPC B
10.1.0.0/16
```

After the appropriate routes and security rules are configured:

```text
EC2 in VPC A
      │
      ↓
Private IP
      │
      ↓
VPC Peering
      │
      ↓
Private IP
      │
      ↓
EC2 in VPC B
```

---

# 🏠 Real-Life Example

Imagine:

```text
🏢 Development Office
```

and:

```text
🏢 Production Office
```

They have separate networks:

```text
Development
10.0.0.0/16

Production
10.1.0.0/16
```

You want:

```text
Development
     ↓
Private Network Connection
     ↓
Production
```

VPC Peering provides the network connection.

But remember:

> **Creating the peering connection alone does not automatically make traffic flow.**

You still need routing and security configuration.

---

# 🧩 Example Architecture

```text
                    ☁️ AWS
                      │
          ┌───────────┴───────────┐
          │                       │
          ↓                       ↓
      ☁️ VPC A                 ☁️ VPC B
    10.0.0.0/16              10.1.0.0/16
          │                       │
        EC2 A                   EC2 B
          │                       │
          └───────────🔗───────────┘
                    Peering
```

---

# 🤔 Why Do We Need VPC Peering?

You might have multiple VPCs for:

```text
Development
Testing
Production
Shared Services
Security
Monitoring
Data
```

Example:

```text
☁️ Dev VPC
       │
       │
       🔗
       │
☁️ Shared Services VPC
```

The Dev VPC might need access to:

```text
DNS
Monitoring
Logging
Internal APIs
Shared tools
```

without putting everything inside one huge VPC.

---

# 🏗️ Example: Development + Shared Services

```text
              🔗 VPC Peering
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
    ☁️ Dev VPC            ☁️ Shared VPC
   10.0.0.0/16            10.1.0.0/16
        │                       │
      EC2                    Monitoring
      EC2                    Logging
```

Now resources in the Dev VPC can communicate privately with permitted resources in the Shared Services VPC.

---

# 🧠 Important Requirement: Non-Overlapping CIDRs

This is one of the most important concepts.

Suppose:

```text
VPC A:
10.0.0.0/16

VPC B:
10.1.0.0/16
```

These ranges do not overlap.

✅ Good.

---

But suppose:

```text
VPC A:
10.0.0.0/16

VPC B:
10.0.0.0/16
```

They overlap.

❌ Problem.

---

# 🚨 Why Is Overlapping CIDR a Problem?

Imagine both VPCs have:

```text
10.0.1.10
```

Which network does:

```text
10.0.1.10
```

belong to?

```text
VPC A?
VPC B?
```

Routing becomes ambiguous.

So for VPC Peering:

> **The VPC CIDR ranges must not overlap.**

---

# 🧠 Good CIDR Design

Example:

```text
VPC A
10.0.0.0/16

VPC B
10.1.0.0/16

VPC C
10.2.0.0/16
```

This makes future network connectivity much easier.

---

# 🛣️ Routing Is Required

This is extremely important.

Suppose:

```text
VPC A:
10.0.0.0/16

VPC B:
10.1.0.0/16
```

You create:

```text
🔗 Peering Connection
```

But:

```text
VPC A Route Table
```

doesn't know where:

```text
10.1.0.0/16
```

is.

Traffic won't magically find the peering connection.

You need a route.

---

# 🛣️ VPC A Route

In VPC A:

```text
Destination:
10.1.0.0/16

Target:
VPC Peering Connection
```

Conceptually:

```text
10.1.0.0/16
       ↓
Peering Connection
```

---

# 🛣️ VPC B Route

You also need the return route.

In VPC B:

```text
Destination:
10.0.0.0/16

Target:
VPC Peering Connection
```

So:

```text
VPC A
10.0.0.0/16
   │
   ↓
Peering
   │
   ↓
VPC B
10.1.0.0/16
```

Both directions need appropriate routing.

---

# 🔄 Complete Routing Example

### VPC A Route Table

```text
Destination       Target

10.0.0.0/16       local
10.1.0.0/16       pcx-xxxx
```

### VPC B Route Table

```text
Destination       Target

10.1.0.0/16       local
10.0.0.0/16       pcx-xxxx
```

Where:

```text
pcx-xxxx
```

represents the VPC peering connection.

---

# 🧠 Think of Routing Like Google Maps

Imagine:

```text
🏠 Home A
```

wants to reach:

```text
🏢 Office B
```

Creating a bridge isn't enough.

Your navigation system also needs to know:

```text
"Take this bridge to reach Office B."
```

That's the route.

---

# 🔥 Security Groups Still Matter

Suppose:

```text
EC2 A
```

wants to connect to:

```text
EC2 B
```

Even if:

```text
VPC Peering ✅
Routes ✅
```

the connection can still fail if the Security Group blocks it.

Example:

```text
EC2 B
Security Group

TCP 8080
Source:
10.0.0.0/16
```

This allows traffic from the VPC A CIDR on port 8080, assuming the rest of the networking path is correctly configured.

---

# 🛡️ NACLs Also Matter

Don't forget:

```text
Security Group
```

and:

```text
Network ACL
```

Both can affect traffic.

Troubleshooting should consider:

```text
Peering
 ↓
Routes
 ↓
Security Group
 ↓
NACL
 ↓
Application
```

---

# 🧩 Complete VPC Peering Flow

Suppose:

```text
EC2 A:
10.0.1.10

EC2 B:
10.1.1.10
```

The application on EC2 A wants to reach:

```text
10.1.1.10:8080
```

Flow:

```text
🖥️ EC2 A
10.0.1.10
     │
     ↓
Route Table
     │
     ↓
10.1.0.0/16
     │
     ↓
🔗 VPC Peering
     │
     ↓
Route Table
     │
     ↓
🛡️ Security Group
     │
     ↓
🖥️ EC2 B
10.1.1.10:8080
```

---

# 🔄 Return Traffic

The return path also matters.

```text
EC2 A
 ↓
VPC Peering
 ↓
EC2 B

EC2 B
 ↓
VPC Peering
 ↓
EC2 A
```

The VPC B route table needs an appropriate route back to:

```text
10.0.0.0/16
```

---

# 🧠 VPC Peering Is Private

VPC Peering provides private network connectivity between VPCs.

Conceptually:

```text
VPC A
  │
  │ Private AWS Network
  │
VPC B
```

You don't need to send the traffic through the public Internet simply to connect the two VPCs.

---

# ⚠️ VPC Peering Is Not a VPN

These are different technologies.

### VPC Peering

```text
VPC A
  ↓
AWS private networking
  ↓
VPC B
```

### VPN

```text
Network A
   ↓
Encrypted VPN Tunnel
   ↓
Network B
```

VPNs are commonly used when connecting networks over a network path such as the Internet.

---

# 🆚 VPC Peering vs VPN

| Feature | VPC Peering | VPN |
|---|---|---|
| Main purpose | Connect VPCs | Connect networks securely |
| Private AWS connectivity | ✅ | Uses VPN tunnel |
| Encryption model | AWS private networking | Encrypted tunnel |
| Typical use | VPC-to-VPC | On-premises ↔ AWS / network connectivity |
| Internet path | Not required for the peering path | Commonly uses Internet for AWS Site-to-Site VPN |

---

# 🔗 VPC Peering Is Not Transitive

This is one of the most important interview concepts.

Suppose:

```text
VPC A
  │
  🔗
  │
VPC B
  │
  🔗
  │
VPC C
```

You might think:

```text
A → B → C
```

means:

```text
A → C
```

automatically.

It does not.

---

# 🚨 Non-Transitive Routing

You need a direct connectivity mechanism between A and C if A needs to communicate with C.

```text
VPC A 🔗 VPC B

VPC B 🔗 VPC C

A ❌→ C automatically
```

This is called:

> **Non-transitive peering**

---

# 🏢 Real-Life Analogy

Imagine:

```text
🏢 Office A
   │
   │
🏢 Office B
   │
   │
🏢 Office C
```

Just because:

```text
A can enter B
B can enter C
```

doesn't automatically mean:

```text
A can enter C
```

unless there is a permitted route.

---

# 🔥 Scaling Problem

Suppose you have:

```text
VPC A
VPC B
VPC C
VPC D
```

You could create multiple peerings:

```text
A ─── B
│ \   │
│  \  │
C ─── D
```

As the number of VPCs grows, managing individual peerings can become complicated.

---

# 📈 Many VPCs

Imagine:

```text
VPC 1
VPC 2
VPC 3
VPC 4
VPC 5
VPC 6
VPC 7
VPC 8
```

Creating lots of individual connections becomes difficult to manage.

This is where a central networking architecture can help.

---

# 🚦 Transit Gateway

AWS provides:

> **Transit Gateway**

Think of it as a central network hub.

```text
               ☁️ VPC A
                  │
                  │
               ☁️ VPC B
                  │
                  ↓
             🚦 Transit
              Gateway
                  ↑
                  │
               ☁️ VPC C
                  │
               ☁️ VPC D
```

Instead of:

```text
A ↔ B
A ↔ C
A ↔ D
B ↔ C
B ↔ D
C ↔ D
```

you can use a hub:

```text
        A
        │
        ↓
B → Transit Gateway ← C
        ↑
        │
        D
```

---

# 🆚 VPC Peering vs Transit Gateway

| Feature | VPC Peering | Transit Gateway |
|---|---|---|
| Connection model | Point-to-point | Hub-and-spoke |
| Best for | Smaller/simple connectivity | Many networks |
| Transitive routing | ❌ | Can support centralized routing |
| Management at scale | More complex | Easier for many networks |
| Architecture | Direct | Central hub |

---

# 🧠 VPC Peering Types

VPC peering can exist:

```text
Same AWS Account
```

or:

```text
Different AWS Accounts
```

and can also connect VPCs across supported AWS Regions.

Conceptually:

```text
Account A
   │
   │
VPC A
   │
   🔗
   │
VPC B
   │
Account B
```

The exact setup and permissions depend on the AWS account/Region configuration.

---

# 🌍 Inter-Region VPC Peering

VPCs can also be connected across AWS Regions using inter-Region VPC peering where supported.

Example:

```text
🇮🇳 Region A
VPC A
10.0.0.0/16
     │
     🔗
     │
🇺🇸 Region B
VPC B
10.1.0.0/16
```

This can allow private communication between resources in different Regions, subject to AWS capabilities, routing, and security configuration.

---

# 🧠 Why Use Inter-Region Peering?

Possible use cases:

```text
Global applications
Disaster recovery
Cross-region services
Data replication
Multi-region architectures
```

---

# 🔐 Security Principle

Just because two VPCs are connected doesn't mean:

```text
Everything → Everything
```

You should still restrict communication.

Example:

```text
VPC A
Application
   │
   │ TCP 443
   ↓
VPC B
API
```

Don't automatically allow:

```text
All Ports
All Protocols
All Resources
```

Use least privilege.

---

# 🏗️ Example: Dev VPC → Shared Services VPC

Suppose:

```text
Dev VPC
10.0.0.0/16
```

and:

```text
Shared Services VPC
10.1.0.0/16
```

Shared services:

```text
Monitoring
Logging
Internal DNS
Artifact Repository
```

Architecture:

```text
              🔗 VPC Peering
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       ☁️ Dev              ☁️ Shared
      VPC                  Services
       │                      │
      EC2                Monitoring
      EC2                Logging
```

The Dev VPC can access only the services it actually needs.

---

# 🏗️ Example: Application VPC → Database VPC

Imagine:

```text
Application VPC
10.0.0.0/16
```

Database:

```text
Database VPC
10.1.0.0/16
```

Architecture:

```text
🌍 Internet
     ↓
Application VPC
     │
     │ 🔗
     ↓
Database VPC
     │
     ↓
🗄️ Database
```

Security:

```text
Application
    ↓
TCP 5432
    ↓
Database
```

Only the required application traffic should be allowed.

---

# 🧠 DNS and VPC Peering

Networking isn't only about IP addresses.

Applications often use names:

```text
database.internal
api.internal
service.internal
```

When connecting VPCs, DNS behavior and name resolution must also be considered.

AWS provides DNS-related options that can be configured for VPC peering.

The important DevOps lesson:

> **Connectivity and name resolution are separate things.**

You can have:

```text
Network connectivity ✅
```

but:

```text
DNS resolution ❌
```

and the application can still fail.

---

# 🚨 Common Troubleshooting Scenario

Your application says:

```text
Connection timed out
```

between:

```text
VPC A
```

and:

```text
VPC B
```

Don't immediately blame the peering connection.

Check:

```text
1️⃣ CIDR overlap
        ↓
2️⃣ Peering status
        ↓
3️⃣ Route tables
        ↓
4️⃣ Security Groups
        ↓
5️⃣ NACLs
        ↓
6️⃣ DNS
        ↓
7️⃣ Application listening port
        ↓
8️⃣ Return route
```

---

# 🔎 Troubleshooting Example

Suppose:

```text
VPC A:
10.0.0.0/16

VPC B:
10.1.0.0/16
```

Application:

```text
10.0.1.10
```

Database:

```text
10.1.1.10:5432
```

Connection fails.

---

## Step 1 — Check Peering

Is:

```text
Peering Status
```

active?

If not:

```text
❌ Fix peering
```

---

## Step 2 — Check VPC A Route

Does VPC A have:

```text
10.1.0.0/16
→ Peering
```

?

If not:

```text
❌ Add route
```

---

## Step 3 — Check VPC B Route

Does VPC B have:

```text
10.0.0.0/16
→ Peering
```

?

If not:

```text
❌ Add return route
```

---

## Step 4 — Check Security Group

Does the database Security Group allow:

```text
TCP 5432
Source: Application VPC/subnet/security group
```

?

If not:

```text
❌ Fix SG
```

---

## Step 5 — Check NACL

Make sure subnet-level rules aren't blocking the connection.

---

## Step 6 — Check Application

Is the database actually listening?

For example:

```text
5432
```

---

# 🧠 Connectivity Checklist

When troubleshooting VPC Peering:

```text
☑ CIDR ranges don't overlap
☑ Peering is active
☑ Route exists on source side
☑ Return route exists
☑ Security Group allows traffic
☑ NACL allows traffic
☑ Destination service is listening
☑ DNS resolves if using hostname
☑ Application configuration is correct
```

---

# 🧪 Hands-on Lab — Design VPC Peering

Don't create expensive AWS resources just for this lab.

Start by designing the network.

---

## VPC A

```text
Name:
Development

CIDR:
10.0.0.0/16
```

Subnet:

```text
10.0.1.0/24
```

---

## VPC B

```text
Name:
Shared-Services

CIDR:
10.1.0.0/16
```

Subnet:

```text
10.1.1.0/24
```

---

# 🧪 Mission 1 — Draw the Architecture

```text
             ☁️ AWS
               │
       ┌───────┴───────┐
       ↓               ↓
   Dev VPC        Shared VPC
10.0.0.0/16      10.1.0.0/16
       │               │
      EC2             EC2
       │               │
       └───────🔗──────┘
          Peering
```

---

# 🧪 Mission 2 — Add Routes

### Dev VPC

```text
Destination:
10.1.0.0/16

Target:
VPC Peering
```

### Shared VPC

```text
Destination:
10.0.0.0/16

Target:
VPC Peering
```

---

# 🧪 Mission 3 — Security

Suppose:

```text
Shared EC2
Port:
8080
```

Allow:

```text
Source:
10.0.0.0/16

Protocol:
TCP

Port:
8080
```

Don't expose unnecessary ports.

---

# 🎮 Challenge

You have:

```text
VPC A:
10.0.0.0/16

VPC B:
10.1.0.0/16
```

Question:

> Can VPC A communicate with VPC B immediately after creating the peering connection?

### Answer:

```text
No ❌
```

You still need appropriate:

```text
Routes
Security Rules
NACL Rules
```

and the destination service must be reachable/listening.

---

# 🎮 Challenge 2

You have:

```text
VPC A
10.0.0.0/16

VPC B
10.0.0.0/16
```

Can you directly establish normal VPC peering between them?

### Answer:

```text
No ❌
```

because the CIDR ranges overlap.

---

# 🎮 Challenge 3

Architecture:

```text
A 🔗 B

B 🔗 C
```

Can A automatically reach C through B?

### Answer:

```text
No ❌
```

VPC Peering is not transitive.

---

# 🎮 Challenge 4

You have:

```text
10.0.0.0/16
```

and:

```text
10.1.0.0/16
```

Which route should VPC A use to reach VPC B?

```text
10.1.0.0/16
```

Target:

```text
VPC Peering Connection
```

---

# 🧠 VPC Peering Cheat Sheet

```text
🔗 VPC Peering
→ Private VPC-to-VPC connectivity

📍 CIDR
→ Must not overlap

🛣️ Routes
→ Required on both sides

🛡️ Security Groups
→ Still apply

🔥 NACLs
→ Still apply

🔄 Return Route
→ Required

🚫 Transitive
→ Peering is not transitive

🌍 Inter-Region
→ Supported for VPC peering where applicable

👥 Cross-Account
→ Supported with appropriate configuration

🚦 Transit Gateway
→ Better for many connected networks
```

---

# 💼 Interview Corner

### Q: What is VPC Peering?

> VPC Peering is a networking connection between two VPCs that allows resources in the VPCs to communicate using private IP addressing, subject to routing and security configuration.

---

### Q: Do VPCs need non-overlapping CIDRs for peering?

> Yes. Overlapping CIDR ranges prevent the routing from being unambiguous.

---

### Q: Is VPC Peering transitive?

```text
No ❌
```

---

### Q: If VPC A is peered with VPC B and VPC B is peered with VPC C, can A communicate with C through B?

```text
Not automatically.
```

You need an appropriate direct connectivity architecture.

---

### Q: Is creating a VPC Peering connection enough?

```text
No.
```

You also need:

```text
Routes
Security Groups
NACLs where applicable
```

and the destination service must be available.

---

### Q: What is the biggest CIDR planning issue with VPC Peering?

> Overlapping CIDR ranges.

---

### Q: What is the difference between VPC Peering and Transit Gateway?

```text
VPC Peering
→ Direct point-to-point connection

Transit Gateway
→ Central hub for connecting multiple networks
```

---

### Q: Can VPC Peering connect VPCs in different AWS accounts?

```text
Yes.
```

The exact process requires the appropriate account permissions and peering acceptance/configuration.

---

### Q: Can VPC Peering work across AWS Regions?

```text
Yes, where inter-Region VPC peering is supported.
```

---

### Q: Does VPC Peering use the public Internet?

> VPC Peering provides private connectivity between VPCs rather than requiring traffic to traverse the public Internet.

---

### Q: What should you check if VPC Peering traffic fails?

```text
CIDR
 ↓
Peering status
 ↓
Route tables
 ↓
Security Groups
 ↓
NACLs
 ↓
Return route
 ↓
DNS
 ↓
Application
```

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain VPC Peering
- [ ] Explain why VPC Peering is used
- [ ] Explain non-overlapping CIDRs
- [ ] Explain VPC peering routes
- [ ] Explain return routes
- [ ] Explain Security Groups with peering
- [ ] Explain NACLs with peering
- [ ] Explain non-transitive peering
- [ ] Explain same-account peering
- [ ] Explain cross-account peering
- [ ] Explain inter-Region peering
- [ ] Compare VPC Peering and VPN
- [ ] Compare VPC Peering and Transit Gateway
- [ ] Explain DNS considerations
- [ ] Troubleshoot VPC Peering connectivity
- [ ] Design a two-VPC architecture
- [ ] Explain least-privilege communication between VPCs

---

# 🎯 Mini Project

## 🔗 Development + Shared Services Network

Design:

```text
                    ☁️ AWS
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
      ☁️ Dev VPC             ☁️ Shared VPC
     10.0.0.0/16             10.1.0.0/16
          │                       │
     🖥️ Application          📊 Monitoring
     🖥️ Application          📝 Logging
          │                       │
          └──────────🔗───────────┘
                   Peering
```

Requirements:

```text
1. Dev VPC must access monitoring.

2. Dev VPC must access logging.

3. Shared Services should not expose unnecessary ports.

4. CIDRs must not overlap.

5. Routes must exist in both directions.

6. Security Groups must restrict access.

7. NACLs should not unintentionally block traffic.

8. Applications should use DNS names where appropriate.
```

Create a table:

| Component | CIDR | Purpose |
|---|---|---|
| Dev VPC | 10.0.0.0/16 | Application workloads |
| Shared VPC | 10.1.0.0/16 | Shared services |

Then document:

```text
Peering Connection:
pcx-xxxx

Dev Route:
10.1.0.0/16 → Peering

Shared Route:
10.0.0.0/16 → Peering
```

---

# 🧠 Final Architecture

```text
                         🌍 AWS
                           │
            ┌──────────────┴──────────────┐
            │                             │
            ↓                             ↓
       ☁️ Dev VPC                  ☁️ Shared VPC
      10.0.0.0/16                 10.1.0.0/16
            │                             │
       ┌────┴────┐                  ┌─────┴─────┐
       ↓         ↓                  ↓           ↓
     App 1     App 2             Logging    Monitoring
       │         │                  │           │
       └────┬────┘                  └─────┬─────┘
            │                             │
            └────────────🔗───────────────┘
                    VPC Peering
```

Traffic:

```text
Dev Application
      ↓
Route Table
      ↓
VPC Peering
      ↓
Shared Services
```

Security:

```text
Route
  ↓
Security Group
  ↓
NACL
  ↓
Application
```

---

# 🔥 DevOps Connection

VPC Peering is your first step toward thinking about **multi-network cloud architecture**.

So far:

```text
One VPC
   ↓
Subnets
   ↓
Routing
   ↓
Security
```

Now:

```text
VPC A
  ↓
VPC Peering
  ↓
VPC B
```

At larger scale:

```text
             VPC A
               │
               ↓
VPC B → 🚦 Transit Gateway ← VPC C
               ↑
               │
             VPC D
```

And eventually you'll see architectures involving:

```text
☁️ Multiple AWS Accounts
🌍 Multiple Regions
🏢 On-Premises Networks
🔗 VPN
🚦 Transit Gateway
🔌 VPC Endpoints
🌐 DNS
🛡️ Centralized Security
🏗️ Terraform
```

The key DevOps mindset:

```text
Network connectivity
        ≠
Security permission
        ≠
Application availability
        ≠
DNS resolution
```

All four have to be correct.

That's exactly the kind of thinking you'll need when troubleshooting real cloud infrastructure. 🔥

---

# 📚 Navigation

⬅️ Previous: **[13-VPC-and-Networking.md](13-VPC-and-Networking.md)**

➡️ Next: **[15-VPN.md](15-VPN.md)**

🏠 Networking Phase: **[README.md](README.md)**

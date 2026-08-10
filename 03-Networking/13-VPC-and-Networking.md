# ☁️ VPC and Cloud Networking

## 🎯 What Are We Learning?

We've built our networking foundation:

```text
IP Address
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
```

Now we're going to put all of those concepts together in the cloud.

Imagine AWS gives you a huge piece of land:

```text
☁️ AWS Cloud
```

You don't want every server in the world to be able to access your machines.

So you create your own isolated network:

```text
🏢 Your Cloud Network
```

In AWS, this is called:

> **VPC — Virtual Private Cloud**

---

# 🧠 What Is a VPC?

A VPC is a logically isolated virtual network that you define inside AWS.

Think of it as:

```text
🏢 Your own private campus
```

Inside the campus you can create:

```text
🏠 Subnets
🛣️ Routes
🚪 Gateways
🔥 Security Controls
🖥️ Servers
⚖️ Load Balancers
```

A simplified architecture:

```text
                         ☁️ AWS
                           │
                           ↓
                     🌐 VPC
                 10.0.0.0/16
                           │
              ┌────────────┴────────────┐
              ↓                         ↓
       🌐 Public Subnet           🔒 Private Subnet
        10.0.1.0/24                10.0.2.0/24
              │                         │
              ↓                         ↓
             EC2                       EC2
```

---

# 🏠 Real-Life Analogy

Imagine a large university campus:

```text
🏫 University
│
├── 🏢 Computer Science
├── 🏢 Administration
├── 🏢 Library
└── 🏢 Hostel
```

The entire campus is:

```text
VPC
```

Individual sections are:

```text
Subnets
```

Roads between them are:

```text
Routing
```

Security gates are:

```text
Security Controls
```

Internet entrance:

```text
Internet Gateway
```

Private outbound exit:

```text
NAT Gateway
```

---

# 🌐 Why Do We Need a VPC?

Without network isolation, cloud resources would be much harder to organize securely.

A VPC lets you design:

```text
Who can communicate?
Where can traffic go?
Which resources are public?
Which resources are private?
Which ports are allowed?
How does Internet traffic enter?
How does private traffic leave?
```

For example:

```text
🌍 Internet
      │
      ↓
⚖️ Load Balancer
      │
      ↓
🖥️ Application
      │
      ↓
🗄️ Database
```

You can place these resources in different network segments.

---

# 🧩 VPC Building Blocks

A typical AWS VPC architecture includes:

```text
VPC
│
├── CIDR Block
│
├── Availability Zones
│
├── Subnets
│
├── Route Tables
│
├── Internet Gateway
│
├── NAT Gateway
│
├── Security Groups
│
├── Network ACLs
│
└── Network Interfaces
```

Later you'll also encounter:

```text
VPC Endpoints
VPC Peering
Transit Gateway
VPN
Direct Connect
```

---

# 📍 VPC CIDR

When creating a VPC, you choose an IPv4 CIDR block.

Example:

```text
10.0.0.0/16
```

This defines the IPv4 address range available within the VPC.

Think:

```text
VPC
10.0.0.0/16
```

Then divide it into smaller networks.

---

# 🧩 VPC Subnets

Suppose:

```text
VPC:
10.0.0.0/16
```

You can create:

```text
Public Subnet:
10.0.1.0/24

Private Subnet:
10.0.2.0/24

Database Subnet:
10.0.3.0/24
```

Visual:

```text
☁️ VPC
10.0.0.0/16
│
├── 🌐 Public
│   10.0.1.0/24
│
├── 🔒 Private
│   10.0.2.0/24
│
└── 🗄️ Database
    10.0.3.0/24
```

---

# 🧠 What Is a Subnet?

A subnet is a logical subdivision of an IP network.

We already learned subnetting.

Now we're applying it to cloud infrastructure.

```text
Large Network
      ↓
Smaller Networks
      ↓
Subnets
```

---

# 🌐 Public vs Private Subnet

This is an extremely important concept.

A subnet is commonly called **public** when its routing configuration provides a path to an Internet Gateway.

A subnet is commonly called **private** when it does not have a direct route to an Internet Gateway.

Example:

```text
🌐 Public Subnet
      │
      ↓
Internet Gateway
      │
      ↓
🌍 Internet
```

Private:

```text
🔒 Private Subnet
      │
      ↓
NAT Gateway
      │
      ↓
Internet Gateway
      │
      ↓
🌍 Internet
```

---

# ⚠️ Important

A subnet does not become public simply because:

```text
"An EC2 has a public IP."
```

The subnet's routing configuration matters.

A useful mental model:

```text
Public Subnet
→ Route to Internet Gateway

Private Subnet
→ No direct route to Internet Gateway
```

---

# 🌐 Internet Gateway

An:

```text
Internet Gateway
```

provides a path between a VPC and the Internet for resources that have appropriate routing and addressing.

Example:

```text
🌍 Internet
      │
      ↓
🌐 Internet Gateway
      │
      ↓
☁️ VPC
```

---

# 🏠 Real-Life Analogy

Imagine your company campus:

```text
🏢 Campus
    │
    ↓
🚪 Main Gate
    │
    ↓
🌍 Public Road
```

The main gate is like the:

```text
Internet Gateway
```

It provides connectivity between the VPC and the Internet.

---

# 🛣️ Route Tables

A route table tells AWS where network traffic should be sent.

Example:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         igw-xxxx
```

Meaning:

```text
10.0.0.0/16
      ↓
Keep traffic inside VPC

0.0.0.0/0
      ↓
Send other IPv4 traffic to Internet Gateway
```

---

# 🌐 Public Route Table

Example:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

Visual:

```text
Public Subnet
      │
      ↓
Route Table
      │
      ↓
Internet Gateway
      │
      ↓
🌍 Internet
```

---

# 🔒 Private Route Table

A private subnet that needs outbound Internet access might have:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         NAT Gateway
```

Visual:

```text
Private Subnet
      │
      ↓
Route Table
      │
      ↓
NAT Gateway
      │
      ↓
Internet Gateway
      │
      ↓
🌍 Internet
```

---

# 🔄 NAT Gateway

We learned NAT earlier.

AWS provides:

> **NAT Gateway**

A NAT Gateway is commonly used to allow resources in private subnets to initiate outbound connections to the Internet without giving those resources public IPv4 addresses.

Example:

```text
🔒 Private EC2
10.0.2.10
      │
      ↓
NAT Gateway
      │
      ↓
Internet Gateway
      │
      ↓
🌍 Internet
```

---

# 🚫 What NAT Gateway Does NOT Do

A NAT Gateway is not a mechanism for arbitrary unsolicited inbound Internet connections to private instances.

Don't think:

```text
Internet
   ↓
NAT Gateway
   ↓
Private EC2
```

as a normal inbound access path.

Instead:

```text
Private EC2
   ↓
NAT Gateway
   ↓
Internet
```

for outbound connections.

---

# ⚖️ Public vs Private Architecture

A common architecture:

```text
                         🌍 Internet
                              │
                              ↓
                       🌐 Internet Gateway
                              │
                              ↓
                     🌐 Public Subnet
                              │
                         ⚖️ ALB
                              │
                    ┌─────────┴─────────┐
                    ↓                   ↓
             🔒 Private Subnet   🔒 Private Subnet
                    │                   │
                  EC2                  EC2
                    │                   │
                    └─────────┬─────────┘
                              ↓
                       🗄️ Database
```

Outbound:

```text
Private EC2
     ↓
NAT Gateway
     ↓
Internet Gateway
     ↓
Internet
```

---

# 🗺️ Availability Zones

AWS regions contain multiple:

```text
Availability Zones
```

For example:

```text
Region
ap-south-1
│
├── AZ 1
├── AZ 2
└── AZ 3
```

A common highly available architecture spreads resources across multiple Availability Zones.

---

# 🏗️ Multi-AZ Architecture

Instead of:

```text
Region
  │
  └── AZ
       │
       └── Server
```

use:

```text
                🌍 Users
                    │
                    ↓
                ⚖️ Load Balancer
                  /       \
                 ↓         ↓
              AZ-1       AZ-2
               │           │
              EC2         EC2
```

If one Availability Zone experiences an issue, resources in another AZ may continue serving traffic.

---

# 🧠 Region vs Availability Zone

### Region

A geographic AWS location containing multiple Availability Zones.

Example:

```text
ap-south-1
```

### Availability Zone

An isolated location within an AWS Region.

Think:

```text
🌍 Region
│
├── 🏢 AZ-1
├── 🏢 AZ-2
└── 🏢 AZ-3
```

---

# 🌐 Subnets and Availability Zones

In AWS, a subnet is associated with a single Availability Zone.

For example:

```text
VPC
│
├── Public Subnet A
│      └── AZ-1
│
├── Public Subnet B
│      └── AZ-2
│
├── Private Subnet A
│      └── AZ-1
│
└── Private Subnet B
       └── AZ-2
```

This is why multi-AZ architectures usually create multiple subnets.

---

# 🔥 Security Groups

Security Groups act as stateful virtual firewalls for supported AWS resources.

Example:

```text
EC2
 │
 ↓
Security Group
```

Rules can control:

```text
Protocol
Port
Source
Destination
```

Example:

```text
TCP 443
Source: 0.0.0.0/0
```

allows HTTPS traffic from IPv4 sources, subject to the resource and networking configuration.

---

# 🛡️ Network ACL

A Network ACL operates at the subnet level.

Example:

```text
Subnet
   │
   ↓
NACL
   │
   ↓
Resources
```

Remember:

```text
Security Group
→ Stateful
→ Resource/network-interface level

NACL
→ Stateless
→ Subnet level
```

---

# 🧠 Security Layers

A cloud architecture can have multiple security layers:

```text
🌍 Internet
      ↓
🔥 WAF
      ↓
⚖️ Load Balancer
      ↓
🛡️ Security Group
      ↓
🖥️ Application
      ↓
🛡️ Security Group
      ↓
🗄️ Database
```

Security is layered.

There should not be one giant firewall rule that says:

```text
"Trust everything." 😂
```

---

# 🔌 Network Interfaces

AWS resources communicate through:

```text
Elastic Network Interfaces
```

commonly called:

```text
ENI
```

An ENI can have network attributes such as:

```text
Private IP addresses
Security Groups
MAC address
Subnet association
```

Conceptually:

```text
EC2
 │
 ↓
ENI
 │
 ↓
Subnet
 │
 ↓
VPC
```

---

# 🌐 Public IPv4

A resource can have a public IPv4 address depending on the resource and configuration.

Example:

```text
EC2
Private IP:
10.0.1.10

Public IP:
203.0.113.x
```

The private address is used within the VPC.

The public address provides Internet-facing connectivity when the associated networking configuration permits it.

---

# 🧠 Private IP vs Public IP

```text
Private IP
→ Internal VPC communication

Public IP
→ Internet-facing communication
```

But remember:

> Having a public IP does not automatically make traffic work.

You also need:

```text
Route
Internet Gateway
Security Group
NACL
Application
```

as applicable.

---

# 🏗️ Complete VPC Architecture

Let's put everything together.

```text
                         🌍 Internet
                              │
                              ↓
                       🌐 Internet Gateway
                              │
             ┌────────────────┴────────────────┐
             │                                 │
        🌐 Public Subnet A                🌐 Public Subnet B
             │                                 │
          ⚖️ ALB                            ⚖️ ALB
             │                                 │
             └────────────────┬────────────────┘
                              │
                     🔒 Private Subnets
                       /             \
                      ↓               ↓
                    EC2             EC2
                      │               │
                      └───────┬───────┘
                              ↓
                       🔒 Database
                             
Private outbound:
                             
EC2
 ↓
NAT Gateway
 ↓
Internet Gateway
 ↓
🌍 Internet
```

This is a very common cloud networking pattern.

---

# 🧭 Traffic Flow — User to Application

Suppose a user opens:

```text
https://example.com
```

A simplified path:

```text
1️⃣ DNS
   ↓
Find Load Balancer address

2️⃣ Internet
   ↓
3️⃣ Internet Gateway
   ↓
4️⃣ Load Balancer
   ↓
5️⃣ Application Subnet
   ↓
6️⃣ EC2
```

---

# 🧭 Traffic Flow — Application to Internet

Suppose the application needs to download an update.

```text
EC2
 ↓
Private Route Table
 ↓
NAT Gateway
 ↓
Public Subnet
 ↓
Internet Gateway
 ↓
🌍 Internet
```

---

# 🧭 Traffic Flow — Application to Database

```text
Application EC2
       ↓
Route Table
       ↓
Database Subnet
       ↓
Database
```

Security controls determine whether the connection is allowed.

For example:

```text
EC2 Security Group
        ↓
Database Security Group
        ↓
TCP 5432
```

---

# 🧠 VPC Peering

Suppose you have:

```text
VPC A
10.0.0.0/16

VPC B
10.1.0.0/16
```

You want them to communicate.

You can use:

```text
VPC Peering
```

Conceptually:

```text
☁️ VPC A
10.0.0.0/16
      │
      │ Peering
      │
☁️ VPC B
10.1.0.0/16
```

---

# ⚠️ Important VPC Peering Concept

VPC peering does not automatically configure all required routes for you.

You need appropriate routes in the relevant route tables.

Example:

```text
VPC A Route Table:

10.1.0.0/16
→ Peering Connection
```

And VPC B needs the corresponding route:

```text
10.0.0.0/16
→ Peering Connection
```

Security rules must also allow the traffic.

---

# 🧩 Transit Gateway

Imagine:

```text
VPC A ──┐
VPC B ──┤
VPC C ──┤── Transit Gateway
VPC D ──┘
```

Instead of creating many individual connections, AWS Transit Gateway can act as a central network hub for connecting VPCs and other networks.

This becomes useful at larger scale.

---

# 🏢 Real-Life Analogy

Small office:

```text
Building A ↔ Building B
```

Simple.

But now:

```text
Building A
Building B
Building C
Building D
Building E
Building F
```

Creating every possible direct connection becomes complicated.

A central hub helps:

```text
             Building A
                  │
Building B ── 🏢 Hub ── Building C
                  │
             Building D
```

That's the basic idea behind a transit hub.

---

# 🔐 VPC Endpoints

Sometimes your private resources need to access AWS services.

Instead of sending traffic through the public Internet, you can use:

```text
VPC Endpoints
```

Conceptually:

```text
Private EC2
    │
    ↓
VPC Endpoint
    │
    ↓
AWS Service
```

Examples include access to services such as:

```text
S3
DynamoDB
ECR
Secrets Manager
CloudWatch
```

The exact endpoint type and networking behavior depend on the AWS service.

---

# 🧠 Why VPC Endpoints Matter

Imagine:

```text
Private EC2
    ↓
Internet
    ↓
AWS Service
```

You may instead design:

```text
Private EC2
    ↓
VPC Endpoint
    ↓
AWS Service
```

This can help keep service traffic within AWS networking and reduce dependence on Internet/NAT paths for supported services.

---

# 🏗️ Three-Tier VPC Architecture

A common design:

```text
                    🌍 Internet
                         │
                         ↓
                    🌐 Public
                    Subnets
                         │
                    ⚖️ Load Balancer
                         │
                         ↓
                    🔒 Private
                  Application Subnets
                         │
                         ↓
                    🔒 Private
                    Database Subnets
```

Example:

```text
VPC:
10.0.0.0/16

Public:
10.0.1.0/24
10.0.4.0/24

Application:
10.0.2.0/24
10.0.5.0/24

Database:
10.0.3.0/24
10.0.6.0/24
```

Each pair can be placed in different Availability Zones.

---

# 🔥 Why Separate Subnets?

Segmentation helps organize and control traffic.

Instead of:

```text
Everything
   ↓
One giant subnet
```

use:

```text
Public
   ↓
Load Balancer

Application
   ↓
Backend

Database
   ↓
Data
```

Then apply different:

```text
Routes
Security Groups
NACLs
Policies
```

---

# 🚨 Common Mistakes

## ❌ "Private subnet means no Internet access."

Not necessarily.

A private subnet can have outbound Internet access through:

```text
NAT Gateway
```

while still lacking a direct route to an Internet Gateway.

---

## ❌ "Public subnet means every resource is public."

No.

A resource still needs appropriate:

```text
IP addressing
Route
Security Group
NACL
Application
```

---

## ❌ "Security Group controls the entire subnet."

No.

Security Groups are associated with supported resources/network interfaces.

NACLs operate at the subnet level.

---

## ❌ "NAT Gateway allows inbound traffic."

No.

Its common purpose is:

```text
Private resources
      ↓
Outbound Internet
```

---

## ❌ "VPC automatically routes between every subnet."

AWS VPCs have a default local route for the VPC's CIDR, but traffic still needs appropriate subnet routes and security controls.

---

# 🧪 Hands-on Lab — AWS Architecture Planning

Before creating anything in AWS, design it on paper.

Create:

```text
VPC:
10.0.0.0/16
```

Subnets:

```text
Public-A:
10.0.1.0/24

Public-B:
10.0.4.0/24

Private-A:
10.0.2.0/24

Private-B:
10.0.5.0/24

Database-A:
10.0.3.0/24

Database-B:
10.0.6.0/24
```

---

# 🧪 Mission 1 — Draw the VPC

Create:

```text
                         VPC
                    10.0.0.0/16
                         │
            ┌────────────┴────────────┐
            ↓                         ↓
           AZ-1                      AZ-2
            │                         │
       Public-A                  Public-B
       10.0.1.0/24                10.0.4.0/24
            │                         │
       Private-A                 Private-B
       10.0.2.0/24                10.0.5.0/24
            │                         │
       Database-A                Database-B
       10.0.3.0/24                10.0.6.0/24
```

---

# 🧪 Mission 2 — Design Routes

### Public Route Table

```text
10.0.0.0/16 → local
0.0.0.0/0   → Internet Gateway
```

### Private Route Table

```text
10.0.0.0/16 → local
0.0.0.0/0   → NAT Gateway
```

### Database Route Table

For a highly restricted database subnet, don't automatically add Internet routes just because the database exists.

Think:

```text
Database
 ↓
Only required destinations
```

---

# 🧪 Mission 3 — Security Design

Application:

```text
Allow:
TCP 443 from Load Balancer
```

Database:

```text
Allow:
TCP 5432 from Application
```

SSH:

```text
Allow:
TCP 22 from trusted administration source
```

Think:

```text
Internet
   ↓
ALB
   ↓
Application
   ↓
Database
```

---

# 🎮 VPC Challenge

You have:

```text
VPC:
10.0.0.0/16
```

You need:

```text
Public subnet
Private application subnet
Private database subnet
```

Create three `/24` subnets.

### Possible answer:

```text
Public:
10.0.1.0/24

Application:
10.0.2.0/24

Database:
10.0.3.0/24
```

Then answer:

```text
1. Which subnet has a route to the Internet Gateway?

2. Which subnet could use a NAT Gateway?

3. Which subnet should contain the database?

4. Which resource should normally be the public entry point?

5. Which security group should allow database traffic?
```

---

# 🎮 Architecture Challenge

Design this:

```text
🌍 Internet
     │
     ↓
    DNS
     │
     ↓
    ALB
     │
     ↓
┌───────────────┐
│ Application   │
│ Private       │
└───────────────┘
     │
     ↓
┌───────────────┐
│ Database      │
│ Private       │
└───────────────┘
```

Now add:

```text
NAT Gateway
Internet Gateway
Route Tables
Security Groups
Availability Zones
```

---

# 🧠 VPC Cheat Sheet

```text
☁️ VPC
→ Your isolated virtual network

📍 CIDR
→ IP range of the VPC

🏠 Subnet
→ Smaller network inside VPC

🌐 Public Subnet
→ Route to Internet Gateway

🔒 Private Subnet
→ No direct route to Internet Gateway

🌐 Internet Gateway
→ VPC ↔ Internet connectivity

🔄 NAT Gateway
→ Private subnet → outbound Internet

🛣️ Route Table
→ Determines where traffic goes

🛡️ Security Group
→ Stateful resource-level traffic control

🔥 NACL
→ Stateless subnet-level traffic control

🌍 Region
→ Geographic AWS location

🏢 Availability Zone
→ Isolated location within a Region

🔗 VPC Peering
→ Connect two VPCs

🚦 Transit Gateway
→ Central network hub

🔌 VPC Endpoint
→ Private connectivity to supported AWS services
```

---

# 💼 Interview Corner

### Q: What is a VPC?

> A VPC is a logically isolated virtual network in AWS where you can define IP ranges, subnets, routing, and network security controls.

---

### Q: What is a subnet?

> A subnet is a logical subdivision of a VPC's IP address range and is associated with a single Availability Zone.

---

### Q: What makes a subnet public?

> A subnet is commonly considered public when its route table has a route to an Internet Gateway.

---

### Q: What makes a subnet private?

> A subnet is commonly considered private when it does not have a direct route to an Internet Gateway.

---

### Q: What is an Internet Gateway?

> An Internet Gateway provides a path between a VPC and the Internet for appropriately configured resources.

---

### Q: What is a NAT Gateway?

> A NAT Gateway allows resources in private subnets to initiate outbound connections to the Internet without requiring public IPv4 addresses on those resources.

---

### Q: Can a private subnet access the Internet?

```text
Yes ✅
```

Typically through:

```text
NAT Gateway
```

if the appropriate routes and security controls are configured.

---

### Q: Can the Internet directly initiate a connection to an EC2 in a private subnet through a NAT Gateway?

```text
No ❌
```

A NAT Gateway is primarily used for outbound connections initiated from private resources.

---

### Q: What is a route table?

> A route table contains routes that determine where network traffic should be sent.

---

### Q: What is the difference between a public and private subnet?

```text
Public
→ Route to Internet Gateway

Private
→ No direct route to Internet Gateway
```

---

### Q: What is VPC Peering?

> VPC Peering is a networking connection between two VPCs that allows resources in those VPCs to communicate using private IP addressing, subject to routing and security configuration.

---

### Q: What is a VPC Endpoint?

> A VPC Endpoint provides private connectivity from a VPC to supported AWS services without requiring the traffic to traverse the public Internet.

---

### Q: What is the difference between a Region and Availability Zone?

```text
Region
→ Geographic AWS location

Availability Zone
→ Isolated location within a Region
```

---

### Q: Why use multiple Availability Zones?

> To improve availability and reduce dependence on a single Availability Zone.

---

### Q: What is the difference between Security Groups and NACLs?

```text
Security Group
→ Stateful
→ Resource/interface level
→ Allow rules

NACL
→ Stateless
→ Subnet level
→ Allow + Deny rules
```

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain VPC
- [ ] Explain VPC CIDR
- [ ] Explain subnets
- [ ] Explain public subnets
- [ ] Explain private subnets
- [ ] Explain Availability Zones
- [ ] Explain Regions
- [ ] Explain Internet Gateway
- [ ] Explain NAT Gateway
- [ ] Explain route tables
- [ ] Explain local VPC routing
- [ ] Explain public route tables
- [ ] Explain private route tables
- [ ] Explain Security Groups
- [ ] Explain NACLs
- [ ] Explain ENIs
- [ ] Explain public vs private IPs
- [ ] Explain VPC Peering
- [ ] Recognize Transit Gateway
- [ ] Explain VPC Endpoints
- [ ] Design a three-tier VPC
- [ ] Design a multi-AZ architecture
- [ ] Explain private subnet outbound Internet access
- [ ] Explain how DNS connects to a VPC architecture
- [ ] Explain how load balancers fit into a VPC
- [ ] Explain how firewalls fit into a VPC
- [ ] Troubleshoot basic VPC connectivity problems

---

# 🎯 Mini Project

## ☁️ Design a Production-Style AWS VPC

Create this architecture:

```text
                         🌍 Internet
                              │
                              ↓
                           Route 53
                              │
                              ↓
                      ⚖️ Application
                      Load Balancer
                              │
                ┌─────────────┴─────────────┐
                ↓                           ↓
             AZ-1                         AZ-2
                │                           │
        🔒 Private App A             🔒 Private App B
                │                           │
                └─────────────┬─────────────┘
                              ↓
                    🔒 Database Subnets
                       /             \
                      ↓               ↓
                  🗄️ DB-A           🗄️ DB-B

Private outbound:
App A/B
   ↓
NAT Gateway
   ↓
Internet Gateway
   ↓
🌍 Internet
```

Use:

```text
VPC:
10.0.0.0/16
```

Subnets:

```text
Public-A:
10.0.1.0/24

Private-App-A:
10.0.2.0/24

Private-DB-A:
10.0.3.0/24

Public-B:
10.0.4.0/24

Private-App-B:
10.0.5.0/24

Private-DB-B:
10.0.6.0/24
```

---

# 📝 Project Questions

Answer these in your README/project notes:

```text
1. Why is the Load Balancer in public subnets?

2. Why are application servers in private subnets?

3. Why are databases in private subnets?

4. Why do we need two Availability Zones?

5. How does the application reach the Internet?

6. How does a user reach the application?

7. How does the application reach the database?

8. Which route table does each subnet use?

9. Where would the Internet Gateway be attached?

10. Where would the NAT Gateway be placed?

11. Which Security Groups are required?

12. Why shouldn't the database have a public IP?

13. Where would DNS fit?

14. What happens if one Availability Zone becomes unavailable?
```

---

# 🔥 DevOps Connection

This is where networking starts becoming **cloud infrastructure**.

Everything we've learned now connects:

```text
                    🌍 Internet
                         │
                         ↓
                       DNS
                         │
                         ↓
                    🔥 WAF
                         │
                         ↓
                  ⚖️ Load Balancer
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
           AZ-1                    AZ-2
              │                     │
        🔒 Private App         🔒 Private App
              │                     │
              └──────────┬──────────┘
                         ↓
                  🔒 Database
```

Outbound:

```text
Private Application
        ↓
    Route Table
        ↓
    NAT Gateway
        ↓
 Internet Gateway
        ↓
      Internet
```

And security:

```text
🌍 Internet
     ↓
   WAF
     ↓
   ALB SG
     ↓
 Application SG
     ↓
 Database SG
```

You now have the foundation for understanding:

```text
☁️ AWS VPC
🖥️ EC2
⚖️ Load Balancers
🔄 NAT Gateway
🛡️ Security Groups
🔥 NACLs
🌐 Route 53
🐳 Docker Networking
☸️ Kubernetes Networking
🏗️ Terraform
🚀 CI/CD
🔐 DevSecOps
```

The big mental model:

```text
VPC
│
├── IP Addressing
│
├── Subnets
│
├── Routing
│
├── Gateways
│
├── Security
│
└── Applications
```

When you eventually write Terraform for AWS, you're going to be creating these exact building blocks as code.

That's the bridge from **networking fundamentals → cloud → DevOps → infrastructure as code**. 🔥

---

# 📚 Navigation

⬅️ Previous: **[12-Load-Balancing.md](12-Load-Balancing.md)**

➡️ Next: **[14-VPC-Peering.md](14-VPC-Peering.md)**

🏠 Networking Phase: **[README.md](README.md)**

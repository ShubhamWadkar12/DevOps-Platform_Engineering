# 🔐 VPN — Virtual Private Network

## 🎯 What Are We Learning?

Imagine your company has:

```text
🏢 Office
```

and its infrastructure is running in AWS:

```text
☁️ AWS Cloud
```

The company wants employees and servers to communicate securely.

Instead of sending private traffic openly across the Internet:

```text
🏢 Office
    │
    │ 🌍 Internet
    │
    ↓
☁️ AWS
```

we can create an encrypted tunnel:

```text
🏢 Office
    │
    │ 🔐 Encrypted VPN Tunnel
    │
    ↓
☁️ AWS
```

This is the basic idea behind a:

> **VPN — Virtual Private Network**

---

# 🧠 What Is a VPN?

A VPN creates a secure, logical connection over an underlying network such as the Internet.

Conceptually:

```text
Network A
    │
    │ 🔐 Encrypted Tunnel
    │
    ↓
Network B
```

The underlying Internet may be public, but the VPN tunnel protects the traffic according to the VPN technology and configuration.

---

# 🏠 Real-Life Analogy

Imagine two buildings:

```text
🏢 Building A
```

and:

```text
🏢 Building B
```

There is a public road between them:

```text
🏢 A ───────── 🌍 Public Road ───────── 🏢 B
```

Anyone can potentially observe the road.

Instead, you build a private protected tunnel:

```text
🏢 A
  │
  │ 🔐
  │
  └══════════════════════╗
                         ║
                         ║
  ╔══════════════════════╝
  │
🏢 B
```

The road still exists underneath.

But your communication uses the protected tunnel.

---

# 🌐 Why Do We Need VPNs?

Common use cases include:

```text
🏢 Office → ☁️ AWS
💻 Employee → 🏢 Company Network
☁️ VPC → 🏢 Data Center
🌍 Remote User → Corporate Network
```

VPNs are commonly used when private network connectivity is needed across an underlying network that isn't itself a private physical network.

---

# 🔐 VPN Basic Architecture

```text
               🌍 Internet
                    │
          🔐 Encrypted VPN Tunnel
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
    🏢 Office                ☁️ AWS
   192.168.0.0/16          10.0.0.0/16
```

The two networks can communicate through the VPN when the tunnel, routing, and security configuration are correct.

---

# 🧩 Important VPN Terms

You will encounter:

```text
VPN
Tunnel
Encryption
Authentication
Peer
Gateway
IPsec
IKE
Pre-shared key
Site-to-Site VPN
Remote Access VPN
```

Let's break them down.

---

# 🔐 Encryption

Encryption transforms readable information into protected information.

Conceptually:

```text
Original Data
     ↓
🔐 Encryption
     ↓
Encrypted Data
```

The receiving side can decrypt it when the appropriate cryptographic mechanisms and keys are available.

---

# 🔑 Authentication

Authentication answers:

> "Who are you?"

For a VPN:

```text
VPN Endpoint A
      ↓
"Prove who you are."
      ↓
VPN Endpoint B
```

Authentication helps prevent unauthorized parties from establishing the intended secure connection.

---

# 🤝 VPN Peer

A VPN connection generally involves two endpoints/peers.

For example:

```text
🏢 Office VPN Gateway
          │
          │
          🔐
          │
          ↓
☁️ AWS VPN Gateway
```

Each side participates in establishing and maintaining the VPN connection.

---

# 🚇 VPN Tunnel

A VPN tunnel is a logical path through which protected traffic is transported.

Example:

```text
🏢 Office
    │
    │
    ╞══════════════════════╡
    │    🔐 VPN Tunnel    │
    ╞══════════════════════╡
    │
    ↓
☁️ AWS
```

The physical network underneath may still be:

```text
🌍 Internet
```

---

# 🧠 VPN Does NOT Mean "No Internet"

This is an important distinction.

A VPN may use:

```text
🌍 Internet
```

as the underlying transport.

The VPN creates:

```text
🔐 Protected tunnel
```

over that transport.

So:

```text
Internet
   ↓
VPN Tunnel
   ↓
Private Network Communication
```

---

# 🔥 VPN Types

Two major types you should know:

```text
1️⃣ Site-to-Site VPN

2️⃣ Remote Access VPN
```

---

# 🏢 Site-to-Site VPN

A Site-to-Site VPN connects two networks.

Example:

```text
🏢 Company Network
        │
        │ 🔐
        │
        ↓
      🌍 Internet
        │
        │ 🔐
        ↓
☁️ AWS VPC
```

The users and devices inside the networks can communicate according to routing and security rules.

---

# 💻 Remote Access VPN

Remote Access VPN connects an individual device to a private network.

Example:

```text
💻 Employee Laptop
        │
        │ 🔐 VPN
        ↓
🌍 Internet
        │
        ↓
🏢 Company Network
```

After connecting, the laptop may be able to access permitted internal resources.

---

# 🆚 Site-to-Site vs Remote Access

| Feature | Site-to-Site | Remote Access |
|---|---|---|
| Connects | Networks | Individual client/device |
| Example | Office ↔ AWS | Laptop ↔ Company |
| Typical endpoint | VPN gateway | VPN client |
| Common use | Hybrid cloud | Remote employees |

---

# ☁️ AWS Site-to-Site VPN

AWS provides:

> **AWS Site-to-Site VPN**

It can connect an on-premises network to an AWS VPC using VPN tunnels.

Conceptually:

```text
🏢 On-Premises
     │
     ↓
Customer Gateway
     │
     │ 🔐 VPN
     │
     ↓
🌐 Internet
     │
     │
     ↓
Virtual Private Gateway
     │
     ↓
☁️ VPC
```

AWS also supports architectures using a Transit Gateway as the AWS-side VPN termination point.

---

# 🧩 Customer Gateway

A:

> **Customer Gateway**

represents the customer-side VPN endpoint/device configuration.

It can represent a physical or software VPN appliance in your network.

Conceptually:

```text
🏢 Your Network
      │
      ↓
Customer Gateway
      │
      🔐
      │
      ↓
AWS
```

---

# ☁️ Virtual Private Gateway

A:

> **Virtual Private Gateway (VGW)**

is an AWS-side VPN gateway that can be associated with a VPC.

Conceptually:

```text
🏢 On-Prem
    │
    🔐
    │
    ↓
Virtual Private Gateway
    │
    ↓
☁️ VPC
```

---

# 🚦 Transit Gateway + VPN

At larger scale, AWS can terminate VPN connections on:

> **Transit Gateway**

Example:

```text
                 🏢 Office A
                     │
                     🔐
                     │
                     ↓
                 🚦 Transit
                  Gateway
                /     |     \
               ↓      ↓      ↓
             VPC A   VPC B   VPC C
```

This is useful when you have:

```text
Multiple VPCs
Multiple offices
Multiple networks
```

---

# 🆚 VGW vs Transit Gateway

### Virtual Private Gateway

```text
VPN
 ↓
VGW
 ↓
One VPC
```

### Transit Gateway

```text
VPN
 ↓
Transit Gateway
 ↓
Multiple VPCs / networks
```

For large environments, Transit Gateway can provide a more centralized networking architecture.

---

# 🔐 IPsec

A very important VPN technology is:

> **IPsec**

IPsec is a suite of protocols and standards used to secure IP communications.

It can provide security properties such as:

```text
Confidentiality
Integrity
Authentication
```

---

# 🧠 IPsec Example

Without VPN:

```text
🏢 Office
   │
   │ 🌍 Internet
   │
   ↓
☁️ AWS
```

With IPsec:

```text
🏢 Office
   │
   │
   ╞═══════════════════╡
   │ 🔐 IPsec Tunnel  │
   ╞═══════════════════╡
   │
   ↓
☁️ AWS
```

---

# 🔑 IKE

VPN systems commonly use:

> **IKE — Internet Key Exchange**

IKE is used to negotiate security parameters and establish keys for IPsec.

You may encounter:

```text
IKEv1
IKEv2
```

Modern deployments commonly prefer:

```text
IKEv2
```

when supported and appropriate.

---

# 🧠 Simplified IPsec Establishment

Don't memorize every cryptographic detail yet.

Think:

```text
1️⃣ Identify each other
        ↓
2️⃣ Negotiate security parameters
        ↓
3️⃣ Establish cryptographic keys
        ↓
4️⃣ Create protected tunnel
        ↓
5️⃣ Exchange protected traffic
```

---

# 🔑 Pre-Shared Key

A common authentication method for VPN tunnels is a:

> **Pre-Shared Key (PSK)**

Both sides are configured with a shared secret.

Conceptually:

```text
🏢 VPN Gateway
      │
      │ 🔑 Same Secret
      │
      ↓
☁️ AWS VPN Gateway
```

If the authentication configuration doesn't match:

```text
❌ Tunnel establishment fails
```

---

# 🔐 Encryption vs Authentication

Don't confuse them.

### Encryption

Protects the confidentiality of data.

```text
Can outsiders read it?
```

### Authentication

Verifies identity.

```text
Are you really the expected peer?
```

VPN security commonly needs both.

---

# 🛡️ Integrity

Integrity helps detect whether protected data was modified.

Conceptually:

```text
Sender
  ↓
🔐 Protected Data
  ↓
Network
  ↓
Receiver
  ↓
Verify
```

If the data has been altered unexpectedly:

```text
❌ Integrity check fails
```

---

# 🧩 VPN Tunnel vs Normal Connection

Normal connection:

```text
Client
  ↓
Internet
  ↓
Server
```

VPN:

```text
Client Network
      ↓
VPN Gateway
      ↓
🔐 Encrypted Tunnel
      ↓
VPN Gateway
      ↓
Private Network
```

---

# 🛣️ VPN Needs Routing

This is extremely important.

Creating a VPN tunnel doesn't automatically mean applications know where to send traffic.

Suppose:

```text
Office:
192.168.0.0/16

AWS:
10.0.0.0/16
```

The office needs a route such as:

```text
10.0.0.0/16
→ VPN
```

AWS needs the appropriate route back:

```text
192.168.0.0/16
→ VPN Gateway / Transit Gateway
```

---

# 🔄 Complete VPN Traffic Flow

Suppose:

```text
Office Server:
192.168.1.10
```

needs to access:

```text
AWS Server:
10.0.1.10
```

Flow:

```text
🏢 Server
192.168.1.10
      │
      ↓
Office Route
      │
      ↓
Customer VPN Gateway
      │
      🔐
      │
      ↓
🌍 Internet
      │
      🔐
      │
      ↓
AWS VPN Gateway
      │
      ↓
AWS Route Table
      │
      ↓
☁️ VPC
      │
      ↓
🖥️ Server
10.0.1.10
```

---

# 🧠 Return Traffic

The return path is equally important.

```text
AWS Server
    ↓
AWS Route Table
    ↓
VPN Gateway
    ↓
🔐 VPN Tunnel
    ↓
Office Gateway
    ↓
Office Route
    ↓
Office Server
```

If the return route is missing:

```text
Request → Maybe reaches destination
Response → ❌ Can't find the way back
```

---

# 🔥 VPN + Firewall

A VPN does not automatically bypass security controls.

You still need:

```text
VPN
 ↓
Route
 ↓
Security Group
 ↓
NACL / Firewall
 ↓
Application
```

For example:

```text
Office
  ↓
VPN
  ↓
AWS
  ↓
Security Group
  ↓
TCP 443
  ↓
Application
```

If the Security Group blocks the traffic:

```text
❌ Connection fails
```

---

# 🧠 VPN + DNS

You may have:

```text
Network connectivity ✅
```

but:

```text
DNS resolution ❌
```

Example:

```text
Application tries:

database.internal
```

If the DNS name cannot be resolved:

```text
❌ Application fails
```

Even though the VPN tunnel is perfectly healthy.

So remember:

```text
VPN connectivity
≠
DNS resolution
```

---

# 🏢 Hybrid Cloud

VPN is a major building block of:

> **Hybrid Cloud**

Hybrid cloud means infrastructure exists across environments such as:

```text
🏢 On-Premises
        +
☁️ Cloud
```

Example:

```text
                 🌍 Internet
                      │
                      🔐
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
      🏢 On-Prem              ☁️ AWS
          │                       │
       Servers                  VPC
          │                       │
       Database               Application
```

---

# 🏗️ Real-World Hybrid Architecture

A company may keep:

```text
🏢 On-Premises
├── Legacy Database
├── Internal Services
└── Corporate Systems
```

while AWS contains:

```text
☁️ AWS
├── Application
├── Kubernetes
├── Load Balancer
└── Monitoring
```

VPN:

```text
🏢 On-Prem
     │
     🔐
     │
     ↓
☁️ AWS
```

allows required private communication between the environments.

---

# ☁️ VPN + VPC Peering

These solve different problems.

### VPC Peering

```text
VPC A
  ↓
🔗
  ↓
VPC B
```

Connects:

```text
VPC ↔ VPC
```

### VPN

```text
Network A
  ↓
🔐
  ↓
Network B
```

Often connects:

```text
On-Premises ↔ AWS
```

or other networks.

---

# 🆚 VPC Peering vs VPN

| Feature | VPC Peering | VPN |
|---|---|---|
| Main purpose | VPC ↔ VPC | Network ↔ Network |
| Encryption tunnel | Not a VPN tunnel | ✅ |
| Common use | AWS VPC connectivity | Hybrid connectivity |
| Internet used as transport | Not required | Commonly |
| Example | VPC A ↔ VPC B | Office ↔ AWS |

---

# 🆚 VPN vs Public Internet

Suppose you have:

```text
🏢 Office
   ↓
🌍 Internet
   ↓
☁️ AWS
```

Traffic travels over a public network.

With VPN:

```text
🏢 Office
   ↓
🔐 Encrypted VPN
   ↓
🌍 Internet
   ↓
🔐 Encrypted VPN
   ↓
☁️ AWS
```

The Internet is still the transport.

The VPN protects the tunnel according to its security configuration.

---

# 💻 Remote Access VPN

Imagine you're working from home.

```text
🏠 Home
   │
   ↓
💻 Laptop
   │
   🔐 VPN
   │
   ↓
🏢 Company Network
```

After authentication, your device may receive access to permitted internal resources.

Example:

```text
GitLab
Internal Dashboard
Internal DNS
Private Servers
```

---

# 🧑‍💻 Developer Example

You're working remotely.

You need to access:

```text
git.company.internal
```

It's not publicly accessible.

You connect:

```text
💻 Laptop
   ↓
🔐 Corporate VPN
   ↓
🏢 Company Network
   ↓
Internal DNS
   ↓
git.company.internal
```

Now the hostname can resolve and the network route can reach the internal service, assuming access is permitted.

---

# 🚨 VPN Troubleshooting

Suppose:

> "The VPN is connected, but I can't access the application."

Don't immediately reconnect the VPN 17 times. 😂

Troubleshoot systematically.

---

## 1️⃣ Is the Tunnel Up?

Check:

```text
VPN Status
```

If:

```text
DOWN
```

investigate:

```text
Authentication
IKE
IPsec
Configuration
Internet connectivity
```

---

## 2️⃣ Is the Route Present?

Check:

```bash
ip route
```

Look for the destination network.

Example:

```text
10.0.0.0/16
```

---

## 3️⃣ Is DNS Working?

Test:

```bash
dig internal.example.com
```

or:

```bash
nslookup internal.example.com
```

---

## 4️⃣ Is the Port Reachable?

For example:

```bash
nc -vz 10.0.1.10 443
```

or:

```bash
curl -v https://10.0.1.10
```

---

## 5️⃣ Check Firewall

Check:

```text
Host Firewall
Security Group
NACL
Network Firewall
```

---

## 6️⃣ Check Application

Is the application actually listening?

```bash
ss -lntup
```

---

# 🧠 VPN Troubleshooting Flow

```text
VPN Tunnel
    ↓
Routing
    ↓
DNS
    ↓
Firewall
    ↓
Port
    ↓
Application
```

If one layer fails:

```text
🚨 Connection fails
```

---

# 🧪 Linux VPN Investigation

Useful commands include:

```bash
ip addr
```

View interfaces.

```bash
ip route
```

View routing.

```bash
ss -lntup
```

View listening sockets.

```bash
ping <IP>
```

Test basic reachability where ICMP is permitted.

```bash
traceroute <IP>
```

Investigate path where supported.

```bash
dig <hostname>
```

Test DNS.

---

# ⚠️ Ping Is Not the Final Test

Suppose:

```text
ping 10.0.1.10
```

fails.

That doesn't automatically mean the server is unreachable.

ICMP may be blocked.

Instead test the actual service:

```bash
nc -vz 10.0.1.10 443
```

or:

```bash
curl -v https://10.0.1.10
```

The correct test depends on the application.

---

# 🧪 Hands-on Lab

## Mission 1 — Understand Your Routes

Run:

```bash
ip route
```

Identify:

```text
Default route
Local network
Interface
```

---

# Mission 2 — Understand Interfaces

Run:

```bash
ip addr
```

Identify:

```text
Loopback
Network interfaces
IPv4 addresses
```

---

# Mission 3 — Simulate VPN Architecture

Draw:

```text
🏢 Office
192.168.0.0/16
       │
       │
       🔐 VPN
       │
       ↓
☁️ AWS VPC
10.0.0.0/16
```

Then document:

```text
Office Route:
10.0.0.0/16 → VPN

AWS Route:
192.168.0.0/16 → VPN
```

---

# 🎮 VPN Challenge

You have:

```text
Office:
192.168.0.0/16

AWS:
10.0.0.0/16
```

The VPN tunnel is:

```text
UP ✅
```

But the office cannot reach:

```text
10.0.2.10
```

What should you check?

### Answer:

```text
1. Office route
2. AWS route table
3. VPN configuration
4. Security Group
5. NACL
6. Firewall
7. Return route
8. Application/service
```

---

# 🎮 Challenge 2

VPN is:

```text
UP ✅
```

You can reach:

```text
10.0.2.10
```

but:

```bash
dig database.internal
```

fails.

What is probably wrong?

```text
DNS configuration/resolution
```

Not necessarily the VPN tunnel itself.

---

# 🎮 Challenge 3

VPN is:

```text
UP ✅
```

DNS works:

```text
database.internal → 10.0.2.10
```

But:

```text
TCP 5432
```

fails.

What should you investigate?

```text
Route
Security Group
NACL
Firewall
Database listener
Database configuration
```

---

# 🧠 VPN Cheat Sheet

```text
🔐 VPN
→ Secure logical connection over an underlying network

🏢 Site-to-Site VPN
→ Network ↔ Network

💻 Remote Access VPN
→ Client ↔ Private Network

🔒 IPsec
→ Protocol suite for securing IP communications

🔑 IKE
→ Negotiates security parameters and keys

🔑 PSK
→ Pre-shared authentication secret

🚇 Tunnel
→ Logical protected path

🛣️ Routing
→ Determines where traffic goes

☁️ AWS Site-to-Site VPN
→ On-premises ↔ AWS

🚦 Transit Gateway
→ Central VPN/network hub

🌐 Hybrid Cloud
→ On-premises + Cloud
```

---

# 💼 Interview Corner

### Q: What is a VPN?

> A VPN creates a secure logical connection over an underlying network such as the Internet, allowing protected communication between endpoints or networks.

---

### Q: What is Site-to-Site VPN?

> A Site-to-Site VPN connects two networks through VPN gateways, commonly using an encrypted tunnel.

---

### Q: What is Remote Access VPN?

> A Remote Access VPN connects an individual client device to a private network.

---

### Q: What is IPsec?

> IPsec is a suite of protocols and standards used to secure IP communications.

---

### Q: What is IKE?

> IKE is used to negotiate security parameters and establish cryptographic keys for IPsec communication.

---

### Q: What is a VPN tunnel?

> A VPN tunnel is a logical protected communication path established between VPN endpoints.

---

### Q: Does a VPN replace routing?

```text
No ❌
```

You still need appropriate routes.

---

### Q: Does a VPN bypass Security Groups?

```text
No ❌
```

Security controls still apply.

---

### Q: VPC Peering vs VPN?

```text
VPC Peering
→ VPC ↔ VPC

VPN
→ Network ↔ Network
→ Encrypted tunnel
```

---

### Q: What is hybrid cloud?

> Hybrid cloud combines on-premises infrastructure with cloud infrastructure and provides connectivity between them when required.

---

### Q: What is AWS Site-to-Site VPN?

> AWS Site-to-Site VPN provides encrypted VPN connectivity between a customer network and an AWS VPC.

---

### Q: What is the role of a Customer Gateway?

> It represents the customer-side VPN endpoint or configuration used for the VPN connection.

---

### Q: What is a Virtual Private Gateway?

> A Virtual Private Gateway is an AWS-side VPN gateway that can be attached to a VPC for VPN connectivity.

---

### Q: Can a VPN tunnel be up while an application is still unreachable?

```text
Yes ✅
```

Because:

```text
Tunnel
 ↓
Routing
 ↓
Security
 ↓
DNS
 ↓
Port
 ↓
Application
```

can fail independently.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain VPN
- [ ] Explain VPN tunnels
- [ ] Explain encryption
- [ ] Explain authentication
- [ ] Explain integrity
- [ ] Explain Site-to-Site VPN
- [ ] Explain Remote Access VPN
- [ ] Explain IPsec
- [ ] Explain IKE
- [ ] Explain pre-shared keys
- [ ] Explain Customer Gateway
- [ ] Explain Virtual Private Gateway
- [ ] Explain AWS Site-to-Site VPN
- [ ] Explain VPN with Transit Gateway
- [ ] Explain hybrid cloud
- [ ] Explain VPN vs VPC Peering
- [ ] Explain VPN vs public Internet
- [ ] Explain VPN routing
- [ ] Explain VPN + Security Groups
- [ ] Explain VPN + DNS
- [ ] Troubleshoot a VPN connection
- [ ] Understand VPN route requirements
- [ ] Understand return routes
- [ ] Explain common VPN failure scenarios

---

# 🎯 Mini Project

## 🏢 Hybrid Cloud VPN Architecture

Design a company network where:

```text
🏢 On-Premises
192.168.0.0/16

        │
        │ 🔐 Site-to-Site VPN
        │
        ↓

☁️ AWS VPC
10.0.0.0/16
```

AWS contains:

```text
Public Subnet
Private Application Subnet
Private Database Subnet
```

Architecture:

```text
                         🏢 Company
                      192.168.0.0/16
                              │
                              🔐
                              │
                         VPN Tunnel
                              │
                              ↓
                    ☁️ AWS VPC
                    10.0.0.0/16
                              │
                  ┌───────────┴───────────┐
                  ↓                       ↓
             Public Subnet          Private Subnet
                  │                       │
                 ALB                    App
                                          │
                                          ↓
                                      Database
```

---

# 📝 Project Questions

Answer these:

```text
1. Why does the company need a VPN?

2. Why should the database remain private?

3. What CIDRs are being used?

4. Why must the CIDRs not overlap?

5. What route should the on-premises network have?

6. What route should AWS have?

7. What happens if the return route is missing?

8. What security controls should protect the application?

9. How would DNS work for internal services?

10. How would you troubleshoot if the VPN tunnel is UP but the application is unreachable?
```

---

# 🔥 DevOps Connection

Look at what you've built conceptually:

```text
🏢 ON-PREMISES
     │
     │ 🔐 VPN
     │
     ↓
☁️ AWS
     │
     ├── VPC
     │
     ├── Subnets
     │
     ├── Route Tables
     │
     ├── Security Groups
     │
     ├── NAT Gateway
     │
     ├── Load Balancer
     │
     └── Applications
```

Now your networking foundation looks much more like real enterprise infrastructure:

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
```

And this leads directly into:

```text
☁️ AWS Networking
🏢 Hybrid Cloud
🚦 Transit Gateway
🔐 Cloud Security
🐳 Docker Networking
☸️ Kubernetes Networking
🏗️ Terraform
🚀 DevOps
🔐 DevSecOps
```

The most important mental model:

```text
VPN
"How do these networks communicate securely?"

Routing
"Where should the traffic go?"

Firewall
"Is the traffic allowed?"

DNS
"What IP/service does this name represent?"

Application
"Is the service actually working?"
```

When something breaks in production, these are the questions you want running through your head automatically. 🔥

---

# 📚 Navigation

⬅️ Previous: **[14-VPC-Peering.md](14-VPC-Peering.md)**

➡️ Next: **[16-Network-Security.md](16-Network-Security.md)**

🏠 Networking Phase: **[README.md](README.md)**

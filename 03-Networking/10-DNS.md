# 🌐 DNS (Domain Name System)

## 🎯 What Are We Learning?

Imagine you want to call your friend.

You remember:

```text
Rahul
```

You don't remember:

```text
+91-XXXXXXXXXX
```

So your phone does the lookup:

```text
👤 Rahul
   ↓
📱 Contacts
   ↓
📞 Phone Number
```

DNS does something conceptually similar for networks:

```text
google.com
     ↓
    DNS
     ↓
IP Address
```

> **DNS = Domain Name System**

DNS is a distributed naming system that helps applications find information associated with domain names.

---

# 🤔 Why Do We Need DNS?

Computers communicate using IP addresses.

For example:

```text
142.250.x.x
```

Imagine having to remember IP addresses for every website:

```text
Google       → ?
GitHub       → ?
Amazon       → ?
YouTube      → ?
ChatGPT      → ?
```

😵‍💫

Instead, we use names:

```text
google.com
github.com
amazon.com
youtube.com
```

DNS helps translate names into information such as IP addresses.

---

# 🏠 Real-Life Analogy

Think about your phone contacts:

```text
"Mom"
  ↓
Phone Number
```

DNS:

```text
"google.com"
  ↓
IP Address
```

So:

```text
Human-friendly name
        ↓
       DNS
        ↓
Machine-usable information
```

---

# 🌐 DNS Is More Than "Domain → IP"

A common beginner explanation is:

> DNS converts domain names into IP addresses.

That's useful, but incomplete.

DNS can store many types of records.

For example:

```text
A
AAAA
CNAME
MX
NS
TXT
SOA
PTR
```

Each has a different purpose.

We'll learn the important ones.

---

# 🧩 DNS Hierarchy

DNS is hierarchical.

Think of it like:

```text
                         .
                    Root DNS
                        │
             ┌──────────┼──────────┐
             ↓          ↓          ↓
            .com       .org       .in
             │
             ↓
          example
             │
             ↓
       www.example.com
```

The hierarchy starts at:

```text
Root
.
```

Then:

```text
Top-Level Domain
.com
.org
.in
```

Then:

```text
Domain
example.com
```

Then possibly:

```text
Subdomain / Host
www.example.com
```

---

# 🌳 DNS Tree

A domain such as:

```text
www.example.com
```

can be thought of as:

```text
.
│
└── com
     │
     └── example
           │
           └── www
```

Read it from right to left:

```text
.
↓
com
↓
example
↓
www
```

---

# 🔤 Domain Name Parts

Take:

```text
www.example.com
```

### `.com`

Top-Level Domain:

```text
TLD
```

### `example`

Registered domain name.

### `www`

Subdomain/host label.

So:

```text
www.example.com
│   │       │
│   │       └── TLD
│   └────────── Domain
└────────────── Host/Subdomain
```

---

# 🌍 Root DNS

At the top of the DNS hierarchy is:

```text
.
```

called the:

```text
Root
```

The root system doesn't normally give you the final IP address directly.

It helps direct queries toward the appropriate top-level domain infrastructure.

For example:

```text
example.com
     ↓
Root
     ↓
.com DNS
     ↓
example.com authoritative DNS
```

---

# 🏷️ Top-Level Domains

Examples:

```text
.com
.org
.net
.in
.dev
.io
```

These are examples of:

```text
Top-Level Domains
```

---

# 🧠 Authoritative DNS Server

An authoritative DNS server contains the authoritative DNS information for a domain or zone.

For example:

```text
example.com
     ↓
Authoritative DNS
     ↓
DNS Records
```

It can provide records such as:

```text
A
AAAA
MX
CNAME
TXT
```

---

# 🔍 Recursive DNS Resolver

Most users don't directly query authoritative servers for every lookup.

Instead, a client usually asks a:

```text
Recursive DNS Resolver
```

Example:

```text
💻 Laptop
    ↓
DNS Resolver
    ↓
Root
    ↓
TLD
    ↓
Authoritative DNS
    ↓
Answer
    ↓
💻 Laptop
```

The resolver does the work of finding the answer.

---

# 🧠 Recursive vs Authoritative

This distinction is important.

### Recursive Resolver

> Finds the answer on behalf of the client.

### Authoritative Server

> Provides the authoritative DNS data for the domain/zone it serves.

Think:

```text
💻 You
 ↓
"Find me google.com"

Recursive Resolver
 ↓
"I'll find it."

Authoritative DNS
 ↓
"Here is the authoritative answer."
```

---

# 🔄 DNS Resolution

Let's say you enter:

```text
www.example.com
```

Your computer needs an IP address.

A simplified process:

```text
💻 Client
   ↓
Recursive Resolver
   ↓
Root DNS
   ↓
.com DNS
   ↓
Authoritative DNS
   ↓
IP Address
   ↓
💻 Client
```

The actual process can vary because of caching and resolver behavior.

---

# ⚡ DNS Caching

Imagine you ask:

> "What's the address of my friend's house?"

You ask once.

Then you write it down.

Next time:

```text
"Where does Rahul live?"

📒 Notes
   ↓
Already know!
```

DNS resolvers and clients can cache DNS answers.

This makes subsequent lookups faster and reduces unnecessary DNS traffic.

---

# ⏱️ TTL

TTL stands for:

```text
Time To Live
```

In DNS, TTL controls how long a cached DNS record can generally be retained before it needs to be refreshed.

Example:

```text
TTL = 300 seconds
```

That's:

```text
5 minutes
```

Another:

```text
TTL = 3600 seconds
```

That's:

```text
1 hour
```

---

# 🚨 Why TTL Matters

Suppose your website changes IP:

```text
Old:
203.0.113.10

New:
203.0.113.20
```

But users may still receive the old address while cached DNS data remains valid.

That's why DNS changes aren't always visible everywhere instantly.

Think:

```text
DNS Record Changed
       ↓
Caches still contain old answer
       ↓
TTL expires
       ↓
Resolver refreshes
       ↓
New answer
```

---

# 🧩 DNS Record Types

Now let's learn the important records.

---

# 1️⃣ A Record

An:

```text
A Record
```

maps a domain name to an IPv4 address.

Example:

```text
example.com
     ↓
A
     ↓
192.0.2.10
```

Remember:

```text
A → IPv4
```

---

# 2️⃣ AAAA Record

An:

```text
AAAA Record
```

maps a domain name to an IPv6 address.

Example:

```text
example.com
     ↓
AAAA
     ↓
2001:db8::10
```

Remember:

```text
A
 ↓
IPv4

AAAA
 ↓
IPv6
```

---

# 🧪 Test A and AAAA

Run:

```bash
dig example.com A
```

Then:

```bash
dig example.com AAAA
```

Compare the answers.

---

# 3️⃣ CNAME

CNAME stands for:

```text
Canonical Name
```

It creates an alias from one DNS name to another DNS name.

Example:

```text
www.example.com
        ↓
CNAME
        ↓
example.com
```

Think:

```text
www
 ↓
"Go ask example.com."
```

---

# ⚠️ CNAME Doesn't Point Directly to an IP

A CNAME points to another DNS name.

Example:

```text
www.example.com
        ↓
CNAME
        ↓
example.com
        ↓
A
        ↓
192.0.2.10
```

---

# 4️⃣ MX Record

MX stands for:

```text
Mail Exchange
```

MX records identify mail servers responsible for receiving email for a domain.

Example:

```text
example.com
     ↓
MX
     ↓
mail.example.com
```

Think:

```text
📧 Email
   ↓
MX
   ↓
📨 Mail Server
```

---

# 5️⃣ NS Record

NS stands for:

```text
Name Server
```

NS records identify the authoritative name servers for a DNS zone.

Example:

```text
example.com
     ↓
NS
     ↓
ns1.example-dns.com
ns2.example-dns.com
```

---

# 6️⃣ TXT Record

TXT records store text associated with a DNS name.

They are commonly used for things such as:

```text
Domain verification
SPF
DKIM-related information
DMARC-related information
```

Example:

```text
example.com
     ↓
TXT
     ↓
"verification=..."
```

---

# 7️⃣ PTR Record

PTR records are used for:

```text
Reverse DNS
```

They map:

```text
IP Address
    ↓
Hostname
```

Normal DNS:

```text
Hostname
    ↓
IP
```

Reverse DNS:

```text
IP
 ↓
Hostname
```

---

# 🔄 Forward vs Reverse DNS

## Forward Lookup

```text
google.com
     ↓
IP Address
```

Example:

```text
example.com
     ↓
192.0.2.10
```

Usually:

```text
A
AAAA
```

---

## Reverse Lookup

```text
192.0.2.10
     ↓
example.com
```

Typically uses:

```text
PTR
```

---

# 🧠 DNS Record Cheat Sheet

| Record | Purpose |
|---|---|
| `A` | Domain → IPv4 |
| `AAAA` | Domain → IPv6 |
| `CNAME` | Alias → another domain name |
| `MX` | Mail servers |
| `NS` | Authoritative name servers |
| `TXT` | Text / verification / email-related data |
| `PTR` | Reverse DNS |
| `SOA` | Zone authority and administrative information |

Remember the big four first:

```text
A
AAAA
CNAME
MX
```

---

# 📧 DNS + Email

When someone sends:

```text
hello@example.com
```

the sending mail system needs to determine:

> "Which mail server handles email for example.com?"

It can query:

```text
MX
```

Example:

```text
example.com
     ↓
MX
     ↓
mail.example.com
```

Then DNS can resolve:

```text
mail.example.com
     ↓
A / AAAA
     ↓
IP Address
```

---

# 🔐 DNS + Security

DNS is also heavily used in security.

For example:

```text
TXT records
```

can be used for domain verification and email authentication mechanisms.

You will later encounter:

```text
SPF
DKIM
DMARC
```

These are especially important for email security.

---

# 🌐 DNS + HTTPS

When you open:

```text
https://example.com
```

a simplified flow is:

```text
1️⃣ DNS
   ↓
Find IP

2️⃣ Routing
   ↓
Find path

3️⃣ TCP
   ↓
Transport connection

4️⃣ TLS
   ↓
Secure connection

5️⃣ HTTPS
   ↓
Web communication
```

DNS happens before the browser can normally connect to the destination using the resolved address.

---

# 🔄 DNS Request Flow

Visualize:

```text
                 💻 Client
                     │
                     │ DNS Query
                     ↓
              🔍 Recursive Resolver
                     │
                     ↓
                 🌳 Root
                     │
                     ↓
                  .com
                     │
                     ↓
          Authoritative DNS
                     │
                     ↓
                IP Address
                     │
                     ↓
                 💻 Client
```

But remember:

> If the resolver already has a valid cached answer, it may not need to query the root, TLD, and authoritative servers again.

---

# 🧠 DNS Query Types

You may hear:

```text
Recursive Query
Iterative Query
```

### Recursive

The resolver is expected to obtain the final answer or an error on behalf of the client.

### Iterative

A DNS server responds with the best information it has, potentially referring the requester to another DNS server.

For your DevOps fundamentals, remember the basic distinction:

```text
Recursive
→ "Find the answer for me."

Iterative
→ "Here is the best information/path I know."
```

---

# 🧪 Linux DNS Tools

There are several useful tools.

---

## `dig`

Probably the most useful tool for DevOps troubleshooting.

```bash
dig example.com
```

---

## Query A

```bash
dig example.com A
```

---

## Query AAAA

```bash
dig example.com AAAA
```

---

## Query MX

```bash
dig example.com MX
```

---

## Query NS

```bash
dig example.com NS
```

---

## Query TXT

```bash
dig example.com TXT
```

---

## Reverse Lookup

```bash
dig -x 8.8.8.8
```

---

# 🔎 `nslookup`

Another common DNS tool:

```bash
nslookup example.com
```

It's simple and available on many systems.

---

# 🔎 `host`

You can also use:

```bash
host example.com
```

Example:

```bash
host example.com
```

It provides a quick DNS lookup.

---

# 🆚 dig vs nslookup vs host

| Tool | Best Use |
|---|---|
| `dig` | Detailed DNS troubleshooting |
| `nslookup` | Simple DNS queries |
| `host` | Quick DNS lookup |

For your DevOps journey:

> **Become comfortable with `dig`.**

---

# 🧪 DNS Investigation Lab

Let's investigate a real domain.

Use:

```bash
dig example.com
```

Look at:

```text
ANSWER SECTION
```

Try:

```bash
dig example.com A
```

Then:

```bash
dig example.com AAAA
```

Then:

```bash
dig example.com MX
```

Then:

```bash
dig example.com NS
```

Then:

```bash
dig example.com TXT
```

You're now inspecting different parts of the domain's DNS configuration.

---

# 🎮 DNS Challenge

Run:

```bash
dig example.com A
```

Question:

```text
What does the A record contain?
```

Answer:

```text
IPv4 address
```

---

# 🎮 Challenge 2

Run:

```bash
dig example.com AAAA
```

Question:

```text
What does AAAA contain?
```

Answer:

```text
IPv6 address
```

---

# 🎮 Challenge 3

Run:

```bash
dig example.com MX
```

Question:

```text
What does MX tell you?
```

Answer:

```text
Which mail servers handle mail for the domain.
```

---

# 🎮 Challenge 4

Run:

```bash
dig example.com NS
```

Question:

```text
What does NS tell you?
```

Answer:

```text
The name servers authoritative for the zone.
```

---

# 🎮 Challenge 5

Run:

```bash
dig -x 8.8.8.8
```

Question:

```text
What type of lookup is this?
```

Answer:

```text
Reverse DNS lookup
```

---

# 🧩 DNS Troubleshooting

Imagine your website isn't opening.

Your application server is healthy.

What could be wrong?

One possibility:

```text
DNS
```

Let's troubleshoot.

---

# 🚨 Scenario 1 — Domain Doesn't Resolve

Run:

```bash
dig example.com
```

If you get:

```text
NXDOMAIN
```

it generally means:

> The queried DNS name does not exist in the DNS namespace being queried.

Potential causes include:

```text
Typo
Missing record
Wrong domain
DNS configuration problem
```

---

# 🚨 Scenario 2 — DNS Works, Website Doesn't

Suppose:

```bash
dig example.com
```

returns an IP.

But:

```bash
curl https://example.com
```

fails.

Then DNS may be working.

Investigate:

```text
DNS
   ↓
IP
   ↓
Route
   ↓
Port 443
   ↓
TLS
   ↓
Application
```

Don't keep changing DNS when DNS is already working.

---

# 🚨 Scenario 3 — Old IP Returned

You changed:

```text
203.0.113.10
```

to:

```text
203.0.113.20
```

But some users still get:

```text
203.0.113.10
```

Think:

```text
DNS Cache
   ↓
TTL
   ↓
Refresh
```

---

# ☁️ DNS in AWS

DNS is everywhere in AWS.

You'll encounter:

```text
Route 53
Private Hosted Zones
Public Hosted Zones
DNS Records
Alias Records
Health Checks
```

For example:

```text
example.com
      ↓
Route 53
      ↓
Load Balancer
      ↓
Application
```

---

# ☁️ AWS Route 53

AWS provides a managed DNS service called:

```text
Amazon Route 53
```

It can be used for:

```text
Domain DNS
DNS routing
Health checks
Traffic management
Private DNS
```

Later, you'll use it with:

```text
EC2
ALB
CloudFront
S3
EKS
```

---

# 🔒 Private DNS

Not all DNS names need to be public.

Imagine an internal company:

```text
db.internal
api.internal
monitoring.internal
```

These may only need to resolve inside a private network.

Conceptually:

```text
Internet
   ❌
    │
Private DNS
    │
🏢 Internal Network
```

Cloud environments commonly use private DNS zones for internal services.

---

# 🐳 DNS + Docker

Docker provides DNS-based service discovery on user-defined networks.

For example:

```text
Docker Network
│
├── web
│
└── database
```

A container can often reach another container using its service/container name on the Docker network.

Conceptually:

```text
web
 ↓
database
 ↓
Docker DNS
 ↓
Database IP
```

This is much better than hard-coding container IP addresses.

---

# ☸️ DNS + Kubernetes

DNS is **extremely important** in Kubernetes.

Imagine:

```text
frontend
   ↓
backend
   ↓
database
```

Kubernetes provides service discovery through DNS.

You can have:

```text
backend.default.svc.cluster.local
```

Conceptually:

```text
Application
    ↓
Service Name
    ↓
Kubernetes DNS
    ↓
Service IP
    ↓
Pods
```

This allows applications to communicate using stable names instead of constantly changing Pod IP addresses.

---

# 🔥 DNS + DevOps

DNS is one of those things you'll touch constantly.

```text
☁️ AWS
   ↓
Route 53

🐳 Docker
   ↓
Container DNS

☸️ Kubernetes
   ↓
Service Discovery

🌐 Websites
   ↓
Domain Names

🔐 Security
   ↓
TXT / DNS-based verification

📧 Email
   ↓
MX / SPF / DKIM / DMARC
```

So yes:

> **DNS is absolutely worth mastering.**

---

# 🧠 DNS Troubleshooting Flow

When someone says:

> 🚨 "The website isn't working!"

Start with:

```text
1️⃣ DNS

dig example.com

        ↓

2️⃣ Does it resolve?

        ↓

3️⃣ Which IP?

        ↓

4️⃣ Can we reach it?

ping IP

        ↓

5️⃣ What route is used?

ip route get IP

        ↓

6️⃣ Is the port reachable?

        ↓

7️⃣ Does HTTPS work?

curl -v https://example.com

        ↓

8️⃣ Is the application healthy?
```

---

# 🧪 Useful Commands Cheat Sheet

```bash
# Basic lookup
dig example.com

# IPv4
dig example.com A

# IPv6
dig example.com AAAA

# Mail servers
dig example.com MX

# Name servers
dig example.com NS

# TXT
dig example.com TXT

# Reverse DNS
dig -x 8.8.8.8

# Simple lookup
nslookup example.com

# Quick lookup
host example.com
```

---

# 🧠 DNS Cheat Sheet

```text
DNS
↓
Domain Name System

A
↓
IPv4

AAAA
↓
IPv6

CNAME
↓
Alias

MX
↓
Mail

NS
↓
Name Servers

TXT
↓
Text / Verification

PTR
↓
Reverse DNS

SOA
↓
Zone Authority Information
```

---

# 🔥 One Important DevOps Concept

Never hard-code dynamic infrastructure IP addresses when a stable DNS name or service-discovery mechanism is appropriate.

Bad:

```text
DATABASE_IP=10.0.2.37
```

If the database changes:

```text
10.0.2.37
      ↓
10.0.2.58
```

your application breaks.

Better:

```text
DATABASE_HOST=db.example.internal
```

Then DNS resolves:

```text
db.example.internal
        ↓
Current IP
```

This is one of the reasons DNS is so important in cloud and DevOps environments.

---

# 💼 Interview Corner

### Q: What is DNS?

> DNS is a distributed hierarchical naming system that maps domain names to information such as IP addresses and mail servers.

---

### Q: What does an A record do?

```text
Domain → IPv4
```

---

### Q: What does an AAAA record do?

```text
Domain → IPv6
```

---

### Q: What is a CNAME?

> A CNAME creates an alias from one DNS name to another DNS name.

---

### Q: What is an MX record?

> An MX record identifies the mail servers responsible for receiving email for a domain.

---

### Q: What is an NS record?

> An NS record identifies name servers authoritative for a DNS zone.

---

### Q: What is a PTR record?

> A PTR record is used for reverse DNS, mapping an IP address to a hostname.

---

### Q: What is TTL?

> TTL specifies how long DNS information can generally be cached before it should be refreshed.

---

### Q: What is DNS caching?

> DNS caching stores previously resolved DNS information temporarily so future queries can be answered faster and with less DNS traffic.

---

### Q: What is a recursive DNS resolver?

> A recursive resolver obtains DNS answers on behalf of clients, potentially querying other DNS servers and using cached results.

---

### Q: What is an authoritative DNS server?

> An authoritative DNS server provides authoritative DNS data for the zones it serves.

---

### Q: What is reverse DNS?

> Reverse DNS resolves an IP address to a hostname, typically using PTR records.

---

### Q: What is the difference between DNS and DHCP?

```text
DNS
→ Name resolution

DHCP
→ Network configuration
```

DNS answers:

> "What address/information is associated with this name?"

DHCP answers:

> "What network configuration should this device use?"

---

### Q: Which command is commonly used for detailed DNS troubleshooting?

```bash
dig
```

---

### Q: Does DNS always use UDP?

```text
No ❌
```

DNS can use:

```text
UDP
TCP
```

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain DNS
- [ ] Explain why DNS is needed
- [ ] Explain DNS hierarchy
- [ ] Explain root DNS
- [ ] Explain TLD
- [ ] Explain authoritative DNS
- [ ] Explain recursive DNS resolvers
- [ ] Explain DNS caching
- [ ] Explain TTL
- [ ] Explain A records
- [ ] Explain AAAA records
- [ ] Explain CNAME
- [ ] Explain MX
- [ ] Explain NS
- [ ] Explain TXT
- [ ] Explain PTR
- [ ] Explain SOA
- [ ] Explain forward DNS
- [ ] Explain reverse DNS
- [ ] Explain recursive vs iterative queries
- [ ] Use `dig`
- [ ] Use `nslookup`
- [ ] Use `host`
- [ ] Query A records
- [ ] Query AAAA records
- [ ] Query MX records
- [ ] Query NS records
- [ ] Query TXT records
- [ ] Perform reverse DNS lookup
- [ ] Troubleshoot basic DNS problems
- [ ] Explain DNS in AWS
- [ ] Explain DNS in Docker
- [ ] Explain DNS in Kubernetes

---

# 🎯 Mini Project

## 🌐 Investigate a Real Domain

Choose a domain such as:

```text
github.com
```

Run:

```bash
dig github.com A
```

```bash
dig github.com AAAA
```

```bash
dig github.com MX
```

```bash
dig github.com NS
```

```bash
dig github.com TXT
```

Then create this table:

| Record | What did you find? | What does it mean? |
|---|---|---|
| A | | IPv4 |
| AAAA | | IPv6 |
| MX | | Mail |
| NS | | Name Servers |
| TXT | | Text / Verification |

Then answer:

```text
1. Which DNS server answered your query?

2. What IPv4 address(es) were returned?

3. What IPv6 address(es) were returned?

4. Does the domain have MX records?

5. Which name servers are authoritative?

6. What TXT records are present?

7. What happens if you query the same domain multiple times?

8. Why can DNS caching make changes appear gradually?
```

---

# 🔥 DevOps Connection

At this point, your networking knowledge is starting to look like real infrastructure knowledge:

```text
                 🌐 NETWORKING

IP Address
    ↓
Subnet
    ↓
Routing
    ↓
NAT
    ↓
Protocols
    ↓
DNS
    ↓
Application
```

Later this becomes:

```text
☁️ AWS
│
├── VPC
├── Subnets
├── Route Tables
├── NAT Gateway
├── Route 53
├── Load Balancer
└── Security Groups

🐳 Docker
│
├── Networks
├── DNS
├── NAT
└── Port Mapping

☸️ Kubernetes
│
├── Pod Networking
├── Services
├── DNS
├── CNI
└── Ingress
```

And when production breaks:

```text
🚨 "API is unreachable!"
```

you won't randomly restart things.

You'll ask:

```text
DNS?
 ↓
IP?
 ↓
Route?
 ↓
NAT?
 ↓
Port?
 ↓
TLS?
 ↓
Application?
```

That's the troubleshooting mindset we're building. 🔥

---

# 📚 Navigation

⬅️ Previous: **[09-Protocols.md](09-Protocols.md)**

➡️ Next: **[11-Firewalls.md](11-Firewalls.md)**

🏠 Networking Phase: **[README.md](README.md)**

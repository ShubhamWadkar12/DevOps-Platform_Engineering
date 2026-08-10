# ⚖️ Load Balancing

## 🎯 What Are We Learning?

Imagine a popular restaurant.

There are:

```text
🍽️ 100 Customers
        │
        ↓
    🧑‍🍳 Kitchen
```

If only one chef handles all 100 orders:

```text
😵‍💫 Chef
   ↓
100 Orders
```

Everything becomes slow.

Instead:

```text
             🍽️ Customers
                   │
                   ↓
             👨‍💼 Host / Manager
              /      |      \
             ↓       ↓       ↓
          👨‍🍳      👨‍🍳      👨‍🍳
         Server 1  Server 2  Server 3
```

The manager distributes customers among available chefs.

In networking, that manager is conceptually similar to a:

> **Load Balancer**

---

# 🧠 What Is Load Balancing?

Load balancing is the process of distributing network traffic across multiple servers or backend resources.

Instead of:

```text
                    🌍 Users
                       │
                       ↓
                    🖥️ Server
                    Server 1
```

we use:

```text
                    🌍 Users
                       │
                       ↓
                 ⚖️ Load Balancer
                  /      |      \
                 ↓       ↓       ↓
              🖥️       🖥️       🖥️
           Server 1  Server 2  Server 3
```

The goal is to avoid depending entirely on one backend server and to distribute traffic appropriately.

---

# 🤔 Why Do We Need Load Balancing?

Suppose your application becomes popular.

Initially:

```text
100 Users
     ↓
🖥️ Server 1
```

Then:

```text
10,000 Users
     ↓
🖥️ Server 1
```

The server may become:

```text
🔥 High CPU
🔥 High Memory
🔥 Slow Responses
🚨 Requests Failing
```

Instead:

```text
10,000 Users
       ↓
  ⚖️ Load Balancer
    /    |    \
   ↓     ↓     ↓
 🖥️    🖥️    🖥️
 S1     S2     S3
```

Traffic can be distributed across multiple servers.

---

# 🏠 Real-Life Analogy

Imagine an airport.

```text
                 👥 Passengers
                      │
                      ↓
               🧑‍✈️ Check-in System
                /      |      \
               ↓       ↓       ↓
            Counter  Counter  Counter
              1        2        3
```

If Counter 1 has a huge queue:

```text
████████████████
```

while Counter 3 is empty:

```text
██
```

the system can direct new passengers to a less busy counter.

That's the basic idea behind load balancing.

---

# 🎯 Main Goals of Load Balancing

Load balancing can help with:

```text
📈 Scalability
⚡ Performance
🛡️ Availability
🔄 Traffic Distribution
🚨 Fault Tolerance
❤️ Health-Based Routing
```

---

# 📈 Scalability

Suppose:

```text
1 Server
```

is no longer enough.

You can add:

```text
Server 2
Server 3
Server 4
```

Then:

```text
Users
  ↓
Load Balancer
  ↓
Multiple Servers
```

This is commonly called:

> **Horizontal Scaling**

---

# 🆚 Vertical vs Horizontal Scaling

## Vertical Scaling

Make one machine bigger.

```text
🖥️ Server
   ↓
More CPU
More RAM
More Storage
```

Example:

```text
4 CPU
16 GB RAM
```

becomes:

```text
16 CPU
64 GB RAM
```

---

## Horizontal Scaling

Add more machines.

```text
🖥️ Server 1
🖥️ Server 2
🖥️ Server 3
```

Traffic:

```text
Users
  ↓
⚖️ Load Balancer
  ↓
Multiple Servers
```

---

# 🆚 Vertical vs Horizontal

| Feature | Vertical Scaling | Horizontal Scaling |
|---|---|---|
| Approach | Bigger machine | More machines |
| Servers | Usually fewer | More |
| Hardware limit | Yes | More flexible |
| Load Balancer | Not necessarily | Commonly used |
| Cloud-native systems | Less flexible | Very common |

---

# 🔥 Availability

Imagine:

```text
⚖️ Load Balancer
    /      \
   ↓        ↓
🖥️ S1     🖥️ S2
```

Suppose:

```text
S1 → ❌ Failed
S2 → ✅ Healthy
```

The load balancer can stop sending new traffic to the unhealthy server if health checks determine that it is unavailable.

So:

```text
Users
  ↓
Load Balancer
  ↓
Healthy Server
```

The application can continue serving traffic.

---

# ❤️ Health Checks

A load balancer can periodically check whether backend servers are healthy.

For example:

```text
GET /health
```

Expected response:

```text
HTTP 200 OK
```

If the backend starts returning errors or becomes unreachable:

```text
🖥️ Server
   ↓
❌ Unhealthy
```

The load balancer can remove it from the active pool.

---

# 🧪 Example Health Check

Suppose your application exposes:

```text
GET /health
```

Response:

```text
200 OK
```

Load balancer:

```text
⚖️
│
├── Server 1 → 200 ✅
├── Server 2 → 200 ✅
└── Server 3 → Timeout ❌
```

Traffic:

```text
Server 1 → Receive
Server 2 → Receive
Server 3 → No new traffic
```

---

# ⚖️ How Does a Load Balancer Decide?

It uses a **load-balancing algorithm** or routing strategy.

Common approaches include:

```text
Round Robin
Weighted Round Robin
Least Connections
IP Hash
Consistent Hashing
```

Different products support different algorithms and behaviors.

---

# 🔄 Round Robin

The simplest example.

Suppose:

```text
Server 1
Server 2
Server 3
```

Requests:

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
Request 5 → Server 2
Request 6 → Server 3
```

Like:

```text
1 → 2 → 3 → 1 → 2 → 3
```

Think:

> "Everyone gets a turn."

---

# ⚖️ Weighted Round Robin

Not all servers are necessarily equal.

Suppose:

```text
Server 1 → Weight 3
Server 2 → Weight 1
```

Server 1 is more powerful.

The load balancer can send proportionally more traffic to it.

Conceptually:

```text
S1
S1
S1
S2
S1
S1
S1
S2
```

The exact distribution depends on the implementation.

---

# 🧠 Least Connections

The load balancer sends a new request toward the backend with fewer active connections, depending on the load balancer's implementation.

Example:

```text
Server 1 → 100 connections
Server 2 → 20 connections
Server 3 → 50 connections
```

A new connection may be directed toward:

```text
Server 2
```

because it currently has fewer active connections.

---

# 🔑 IP Hash

A load balancer can use the client's IP address as an input to determine the backend.

Conceptually:

```text
Client A
   ↓
Hash(Client IP)
   ↓
Server 2
```

The same client may therefore tend to reach the same backend, depending on the implementation.

This can be useful for certain stateful applications.

---

# 🍪 Session Stickiness

Sometimes an application expects a user to continue reaching the same backend.

Example:

```text
User
  ↓
Server 1
```

Then future requests:

```text
User
  ↓
Server 1
```

This is called:

> **Session Affinity** or **Sticky Sessions**

It can be implemented using mechanisms such as cookies or source information depending on the load balancer.

---

# ⚠️ Why Sticky Sessions Can Be a Problem

Suppose:

```text
User
 ↓
Server 1
```

Server 1 crashes:

```text
Server 1 → ❌
```

The user's session may be affected if the application stores important state only on that server.

A more cloud-native design is often:

```text
Load Balancer
     ↓
Any Application Server
     ↓
Shared Database / Cache / Session Store
```

Instead of:

```text
Server 1
   ↓
Only Server 1 knows everything
```

---

# 🧠 Stateless Applications

A stateless application doesn't depend on local server memory for persistent user state.

Example:

```text
User
 ↓
Load Balancer
 ↓
Server 1

Next request
 ↓
Load Balancer
 ↓
Server 2
```

The application still works because the required state is stored elsewhere or included in the request/token.

This makes horizontal scaling much easier.

---

# 🧩 Layer 4 vs Layer 7 Load Balancing

This is very important.

Load balancers can operate at different levels.

---

# 🚚 Layer 4 Load Balancing

Layer 4 works primarily with transport-level information.

Examples:

```text
TCP
UDP
IP
Port
```

It doesn't need to understand the full HTTP request.

Conceptually:

```text
Client
   ↓
TCP :443
   ↓
⚖️ L4 Load Balancer
   ↓
Backend
```

---

# 🌐 Layer 7 Load Balancing

Layer 7 can understand application-level protocols such as HTTP/HTTPS.

It can make decisions based on things like:

```text
Host
Path
Headers
Cookies
HTTP method
```

Example:

```text
example.com/api
        ↓
Backend A

example.com/images
        ↓
Backend B
```

---

# 🆚 L4 vs L7

| Feature | L4 | L7 |
|---|---|---|
| Layer | Transport | Application |
| Understands | IP, TCP/UDP, ports | HTTP/HTTPS details |
| URL path routing | ❌ | ✅ |
| Host-based routing | ❌ | ✅ |
| Usually more application-aware | Less | More |
| Example use | TCP/UDP services | Web applications |

---

# 🏠 Real-Life Example

Imagine a building.

### L4

The receptionist says:

> "Send everyone entering through Door 443 to the appropriate office."

They care about:

```text
Address
Port
Transport
```

### L7

The receptionist asks:

> "What website are you visiting?"

```text
/api
/images
/login
```

Now the receptionist understands the request itself.

That's the difference.

---

# 🌐 Reverse Proxy

A load balancer is often also used as a:

> **Reverse Proxy**

The client communicates with the load balancer rather than directly with the backend server.

```text
Client
  ↓
Reverse Proxy / Load Balancer
  ↓
Backend
```

The backend is hidden behind the proxy from the client's direct perspective.

---

# 🆚 Forward Proxy vs Reverse Proxy

## Forward Proxy

Acts on behalf of clients.

```text
Client
  ↓
Forward Proxy
  ↓
Internet
```

The destination server sees the proxy as the intermediary.

---

## Reverse Proxy

Acts on behalf of servers.

```text
Internet
   ↓
Reverse Proxy
   ↓
Backend Servers
```

The client doesn't directly communicate with the backend server.

---

# 🧠 Easy Memory Trick

```text
Forward Proxy
→ In front of CLIENTS

Reverse Proxy
→ In front of SERVERS
```

---

# 🔐 TLS Termination

A load balancer can sometimes terminate TLS.

Example:

```text
Client
  │
  │ HTTPS
  ↓
⚖️ Load Balancer
  │
  │ HTTP or HTTPS
  ↓
🖥️ Backend
```

The load balancer decrypts the client-side TLS connection.

This is called:

> **TLS Termination**

---

# 🔐 TLS Passthrough

Alternatively, the load balancer may pass encrypted traffic through to the backend.

Conceptually:

```text
Client
  │
  │ HTTPS
  ↓
⚖️ Load Balancer
  │
  │ HTTPS
  ↓
🖥️ Backend
```

The backend handles TLS.

Whether this is supported and how it works depends on the load-balancing technology.

---

# 🧠 Why TLS Termination?

Centralizing TLS at the load balancer can simplify:

```text
Certificate Management
TLS Configuration
Cipher Configuration
Traffic Inspection
```

But it also means:

```text
Load Balancer
      ↓
Decrypted traffic
```

So the architecture needs to consider whether traffic should also be encrypted between the load balancer and backend.

---

# ☁️ AWS Load Balancing

AWS provides several load balancing options through:

> **Elastic Load Balancing (ELB)**

Important types to know:

```text
Application Load Balancer
Network Load Balancer
Gateway Load Balancer
```

---

# 🟢 Application Load Balancer

ALB operates at:

```text
Layer 7
```

It is designed for:

```text
HTTP
HTTPS
```

It supports application-aware routing features such as:

```text
Host-based routing
Path-based routing
Header-based routing
```

---

# 🌐 ALB Example

Suppose:

```text
example.com
```

has:

```text
/api
/images
```

You can conceptually route:

```text
/api
  ↓
Backend API Servers

/images
  ↓
Image Servers
```

Diagram:

```text
                 🌍 Users
                     │
                     ↓
                 ⚖️ ALB
                 /      \
                ↓        ↓
             /api     /images
              ↓          ↓
           API Pool   Image Pool
```

---

# 🔵 Network Load Balancer

AWS Network Load Balancer operates primarily at:

```text
Layer 4
```

It supports:

```text
TCP
TLS
UDP
```

depending on listener configuration.

It is useful when you need high-performance transport-level load balancing and features appropriate to L4 traffic.

---

# 🆚 ALB vs NLB

| Feature | ALB | NLB |
|---|---|---|
| Main Layer | L7 | L4 |
| HTTP/HTTPS aware | ✅ | Can pass/handle TLS but isn't an HTTP-aware L7 router |
| Path-based routing | ✅ | ❌ |
| Host-based routing | ✅ | ❌ |
| TCP | Not the primary use | ✅ |
| UDP | ❌ | ✅ |
| Typical use | Web applications | TCP/UDP/high-performance services |

---

# 🟣 Gateway Load Balancer

Gateway Load Balancer is designed for deploying and scaling network virtual appliances.

Examples include:

```text
Firewalls
Intrusion Detection/Prevention Systems
Traffic inspection appliances
```

Conceptually:

```text
Traffic
   ↓
Gateway Load Balancer
   ↓
Security Appliance Fleet
   ↓
Destination
```

---

# ☁️ AWS Architecture Example

A common web architecture:

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
                    ┌─────────┼─────────┐
                    ↓         ↓         ↓
                  🖥️        🖥️        🖥️
                EC2/ECS    EC2/ECS    EC2/ECS
                    │         │         │
                    └─────────┼─────────┘
                              ↓
                           🗄️ RDS
```

Traffic is distributed across healthy backend targets.

---

# 🐳 Load Balancing + Docker

Suppose you have:

```text
Container 1
Container 2
Container 3
```

You can place a reverse proxy/load balancer in front:

```text
             🌍 Users
                 │
                 ↓
             ⚖️ Proxy
            /    |    \
           ↓     ↓     ↓
          C1    C2    C3
```

Examples of technologies commonly used for this purpose include:

```text
NGINX
HAProxy
Traefik
Envoy
```

---

# ☸️ Load Balancing + Kubernetes

Kubernetes has multiple layers of traffic handling.

A simplified path:

```text
🌍 User
   ↓
Ingress / Gateway
   ↓
Service
   ↓
Pods
```

For example:

```text
                🌍 Users
                    │
                    ↓
              ⚖️ Ingress
                    │
                    ↓
                Service
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
         Pod       Pod       Pod
```

Kubernetes Services provide stable access to changing Pod instances.

Ingress or Gateway APIs can provide HTTP-aware routing.

---

# 🔥 Load Balancing + Kubernetes

Imagine:

```text
Pod 1 → ❌
Pod 2 → ✅
Pod 3 → ✅
```

Traffic should go toward healthy/available endpoints according to the service and ingress/load-balancing implementation.

This is why:

```text
Health
+
Service Discovery
+
Load Balancing
```

are critical in Kubernetes.

---

# 🚨 Real DevOps Scenario

Your company runs:

```text
Website
```

Traffic increases:

```text
100 users
   ↓
1 server

10,000 users
   ↓
1 server → 🔥
```

You deploy:

```text
Server 1
Server 2
Server 3
```

Then:

```text
Users
  ↓
Load Balancer
  ↓
┌───────┬───────┬───────┐
↓       ↓       ↓
S1      S2      S3
```

Now Server 2 crashes:

```text
S1 → ✅
S2 → ❌
S3 → ✅
```

Health checks detect:

```text
S2 → Unhealthy
```

Traffic continues toward:

```text
S1
S3
```

This is one of the key benefits of load balancing.

---

# 🧠 Load Balancer Does NOT Automatically Fix Everything

Suppose:

```text
Database → ❌
```

Your application servers are healthy:

```text
S1 → ✅
S2 → ✅
S3 → ✅
```

The load balancer cannot magically fix:

```text
Database failure
DNS failure
Routing failure
Firewall failure
Application bugs
```

It solves traffic distribution and availability problems within its scope.

---

# 🚨 Common Mistakes

## ❌ "Load Balancer = Backup Server"

No.

A load balancer distributes traffic.

Backend servers provide the application service.

---

## ❌ "Load Balancer makes an application infinitely scalable"

No.

It helps distribute traffic, but you still need:

```text
Capacity Planning
Auto Scaling
Database Scaling
Caching
Efficient Application Design
```

---

## ❌ "Every load balancer works at Layer 7"

No.

Some load balancers operate primarily at:

```text
Layer 4
```

Others at:

```text
Layer 7
```

---

## ❌ "If a server responds to ping, it's healthy"

Not necessarily.

A server could respond to ICMP while:

```text
HTTPS is broken
Application is crashed
Database connection is failing
```

That's why application-aware health checks are useful.

---

# 🧪 Hands-on Lab

## Mission 1 — Check Listening Ports

Run:

```bash
ss -lntup
```

Find a service listening on your system.

Record:

```text
IP:
Port:
Protocol:
Process:
```

---

# Mission 2 — Test HTTP

Run:

```bash
curl -I https://example.com
```

Look at:

```text
HTTP Status
Server
Headers
```

Think:

```text
Client
 ↓
HTTP/HTTPS
 ↓
Server
```

---

# Mission 3 — Create Two Local Web Servers

If you have Python installed:

Terminal 1:

```bash
mkdir -p ~/lb-lab/server1
echo "Hello from Server 1" > ~/lb-lab/server1/index.html
cd ~/lb-lab/server1
python3 -m http.server 8001
```

Terminal 2:

```bash
mkdir -p ~/lb-lab/server2
echo "Hello from Server 2" > ~/lb-lab/server2/index.html
cd ~/lb-lab/server2
python3 -m http.server 8002
```

Now test:

```bash
curl http://127.0.0.1:8001
```

and:

```bash
curl http://127.0.0.1:8002
```

You should see different responses.

You now have:

```text
Server 1 → :8001
Server 2 → :8002
```

---

# 🧪 Mission 4 — Think Like a Load Balancer

Create this architecture on paper:

```text
                  🌍 Client
                      │
                      ↓
                  ⚖️ LB
                 /     \
                ↓       ↓
             :8001    :8002
               │         │
              S1        S2
```

Now imagine:

```text
Request 1 → S1
Request 2 → S2
Request 3 → S1
Request 4 → S2
```

That's the basic idea of round-robin distribution.

---

# 🎮 Load Balancing Challenge

You have:

```text
Server 1 → 10 connections
Server 2 → 2 connections
Server 3 → 7 connections
```

If the load balancer uses a **least-connections** strategy, which server would be preferred for a new connection?

### Answer:

```text
Server 2
```

because it currently has the fewest connections.

---

# 🎮 Challenge 2

You have:

```text
Server 1 → Weight 5
Server 2 → Weight 1
```

Which server should receive more traffic under weighted load balancing?

### Answer:

```text
Server 1
```

because it has the higher configured weight.

---

# 🎮 Challenge 3

You have:

```text
/api/users
/api/orders
/images/logo.png
```

You want:

```text
/api/*      → API Servers
/images/*   → Image Servers
```

Which type of load balancing is appropriate?

### Answer:

```text
Layer 7
```

because the decision depends on the HTTP path.

---

# 🎮 Challenge 4

You need to distribute:

```text
TCP traffic
```

without needing to understand HTTP URLs.

Which type is more appropriate?

### Answer:

```text
Layer 4
```

---

# 🧠 Load Balancing Cheat Sheet

```text
⚖️ Load Balancer
→ Distributes traffic

🔄 Round Robin
→ Rotate through servers

⚖️ Weighted
→ More traffic to higher-weight servers

📉 Least Connections
→ Prefer fewer active connections

🔑 IP Hash
→ Use client IP in backend selection

❤️ Health Check
→ Determine backend availability

🧠 Session Affinity
→ Keep a client associated with a backend

🚚 L4
→ TCP/UDP/IP/ports

🌐 L7
→ HTTP/HTTPS-aware

🔐 TLS Termination
→ LB handles client TLS

🔄 Reverse Proxy
→ Sits in front of backend servers
```

---

# 💼 Interview Corner

### Q: What is load balancing?

> Load balancing distributes network traffic across multiple backend servers or resources to improve availability, scalability, and performance.

---

### Q: Why do we use a load balancer?

> To distribute traffic across multiple backend resources and improve scalability and availability.

---

### Q: What is horizontal scaling?

> Adding more instances or servers to handle increased workload.

---

### Q: What is vertical scaling?

> Increasing the resources of an existing server, such as CPU or memory.

---

### Q: What is a health check?

> A mechanism used to determine whether a backend target is healthy and able to receive traffic.

---

### Q: What is Round Robin?

> A load-balancing strategy that distributes requests sequentially across available backends.

---

### Q: What is Least Connections?

> A strategy that generally directs new connections toward a backend with fewer active connections.

---

### Q: What is Layer 4 load balancing?

> Load balancing based primarily on transport/network information such as IP addresses, TCP/UDP, and ports.

---

### Q: What is Layer 7 load balancing?

> Application-aware load balancing that can make decisions using information such as HTTP hostnames, paths, headers, or cookies.

---

### Q: What is a reverse proxy?

> A server or service that accepts requests on behalf of backend servers and forwards those requests to appropriate backends.

---

### Q: What is TLS termination?

> TLS termination occurs when a load balancer or proxy terminates the client's TLS connection and processes the decrypted traffic.

---

### Q: What is the difference between ALB and NLB?

```text
ALB
→ Layer 7
→ HTTP/HTTPS
→ Path/host-based routing

NLB
→ Layer 4
→ TCP/UDP/TLS use cases
→ High-performance transport-level traffic
```

---

### Q: What is session stickiness?

> Session stickiness, or session affinity, attempts to keep a client's requests associated with the same backend server.

---

### Q: What happens if a backend server fails?

> If health checks detect the server as unhealthy, the load balancer can stop sending new traffic to that backend according to its configuration.

---

# 🏆 What You Should Be Able to Explain

Before moving forward, make sure you can:

- [ ] Explain load balancing
- [ ] Explain why load balancing is needed
- [ ] Explain horizontal scaling
- [ ] Explain vertical scaling
- [ ] Explain availability
- [ ] Explain health checks
- [ ] Explain Round Robin
- [ ] Explain Weighted Round Robin
- [ ] Explain Least Connections
- [ ] Explain IP Hash
- [ ] Explain session affinity
- [ ] Explain stateless applications
- [ ] Explain Layer 4 load balancing
- [ ] Explain Layer 7 load balancing
- [ ] Explain reverse proxy
- [ ] Explain forward vs reverse proxy
- [ ] Explain TLS termination
- [ ] Explain TLS passthrough
- [ ] Explain AWS Elastic Load Balancing
- [ ] Explain Application Load Balancer
- [ ] Explain Network Load Balancer
- [ ] Recognize Gateway Load Balancer
- [ ] Explain load balancing in Docker
- [ ] Explain load balancing in Kubernetes
- [ ] Explain health checks
- [ ] Troubleshoot basic load-balancer problems
- [ ] Explain load balancing in a cloud architecture

---

# 🎯 Mini Project

## 🏗️ Design a Highly Available Web Application

Design this architecture:

```text
                         🌍 Users
                            │
                            ↓
                         🌐 DNS
                            │
                            ↓
                     ⚖️ Load Balancer
                     /       |       \
                    ↓        ↓        ↓
                  🖥️       🖥️       🖥️
                Server 1  Server 2  Server 3
                    │        │        │
                    └────────┼────────┘
                             ↓
                          🗄️ Database
```

Requirements:

```text
1. Users access the application through HTTPS.

2. Traffic is distributed across three servers.

3. Unhealthy servers should stop receiving new traffic.

4. The application should support horizontal scaling.

5. Users should not directly access backend servers.

6. Database access should be restricted to the application tier.

7. DNS should point users toward the public entry point.
```

Create a table:

| Component | Purpose |
|---|---|
| DNS | |
| Load Balancer | |
| Server 1 | |
| Server 2 | |
| Server 3 | |
| Database | |
| Health Check | |
| Firewall/Security Group | |

Then answer:

```text
1. Why do we need a load balancer?

2. What happens if Server 2 fails?

3. Why are health checks important?

4. Why is L7 useful for web applications?

5. When would L4 be preferred?

6. What is the difference between ALB and NLB?

7. Where would TLS terminate?

8. Why should the database not be publicly accessible?

9. How could this architecture scale from 3 servers to 30?

10. What role does DNS play?
```

---

# 🔥 DevOps Connection

Now connect everything we've learned:

```text
                         🌍 Users
                            │
                            ↓
                          DNS
                            │
                            ↓
                     🔥 WAF / Firewall
                            │
                            ↓
                     ⚖️ Load Balancer
                            │
                  ┌─────────┼─────────┐
                  ↓         ↓         ↓
                🖥️        🖥️        🖥️
               App 1      App 2      App 3
                  │         │         │
                  └─────────┼─────────┘
                            ↓
                         🗄️ DB
```

Outbound:

```text
Application
     ↓
Route Table
     ↓
NAT Gateway
     ↓
Internet Gateway
     ↓
🌍 Internet
```

You've now connected:

```text
IP
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
Firewall
 ↓
Load Balancing
```

And this is the foundation for:

```text
☁️ AWS
🐳 Docker
☸️ Kubernetes
🚀 CI/CD
🏗️ Terraform
🔐 DevSecOps
📊 Monitoring
🌐 Platform Engineering
```

The big mental model to keep:

```text
DNS
"Where is the application?"

        ↓

Load Balancer
"Which backend should receive this traffic?"

        ↓

Firewall
"Is this traffic allowed?"

        ↓

Routing
"Where should the packet go?"

        ↓

Application
"Can the service actually handle it?"
```

That's the networking foundation of modern infrastructure. 🔥

---

# 📚 Navigation

⬅️ Previous: **[11-Firewalls.md](11-Firewalls.md)**

➡️ Next: **[13-VPC-and-Networking.md](13-VPC-and-Networking.md)**

🏠 Networking Phase: **[README.md](README.md)**

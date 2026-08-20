# Software Architecture 

## Table of Contents
1. Application Architectures (Code Organization)
- monolithic Architecture
- modular Monolith
- microservices architecture
- serverless / Faas

2. Deployment/System ARchitecture (Infrastructure)
- Client - Server
- 3-Tier Architecture
- N-Tier / Multi - Tier
3. Advanced & Specialized Patterns
- Event-Driven Architecture (EDA)
- Space-Based Architecture
- Peer-to-Peer(P2P)
4. Quick Comparison Matrix
5. Decision Flowchart


### Application Architectures (Code Organization)
These define how you structure your backend code and split responsibilities.

1.1. Monolithic architecture

A single, unified codebase where all business logic, UI, data access, and external integrations are bundled into one deployable unit

**Structure**
[Frontend] → [Single Backend Server] → [Single Database]
                    │
    ┌───────────────┼───────────────┐
    │               │               │
User Module    Payment Module   Inventory Module
(All share same database & codebase)

**Characteristics**
- Single deployment artifact (one JAR/WAR/DLL)
- All modules run in the same process
- Shared database schema across all features
- One technology stack for the entire app

**Pros**
- Simple development - Easy to write, debug, and test locally
- Straightforward - One artifact to ship
- Easy monitoring - One set of logs, one health check
- Low latency - Function calls are in-memory (no netowrk hops)
- ACID(Automicity Consistency Isolation Durability) transactions - Single database = atimic, consistent operations

**Cons**
- Tight coupling - Changing one module can break others
- Scaling inefficiency - Scale the entire app, even if only one feature is overloaded
- Slow development velocity - Large teams create merge conflicts daily
- Long build times - Compiling/tests take hours for enterprise apps
- Technology lock-in ->  Hard to adopt new languages or frameworks
- Single point of failure - One crash takes everything down

**When to Use**
- MVP and early stage startups
- small teams less than 10 devs
- Simple CRUD applications
- Products with stable, non-complex requirements

**Famous Examples**
-Early versions of Amazon, Etsy, and Shopify
- Most Wordpress and Django-based sites

1.2. Modular Monolith
A monolith that is strictly organized into independent, decoupled modules with well-defined boundaries, but still deployed as a single unit.

**Structure**
[Frontend] → [Single Backend Server]
                    │
    ┌───────────────┼───────────────┐
    │               │               │
 User Module    Payment Module  Inventory Module
    │               │               │
  [Private DB]   [Private DB]   [Private DB]
  (Modules communicate via internal APIs, NOT direct DB access)

  **Characteristics**
  - One codebase, but strict module boundaries
  - Each module owns its own database schema
  - Modules communicate thorugh internal API calls (not HTTP)
  - Still deployed as one application

  **pros**
  - All benefits of monolith - Simple deployment, low latency, easy debugging
  - Better organization - Forces clean separation of concerns
  - Future proof - Modules can be extracted into microservices later
  - Database independence - Each module controls its own data

  **cons**
  - still a single deployment (if one module crashes, all crash)
  - still locked into one tech stack
  - requires discipline from the team to maintain boundries

  **When to use**
  - Growing teams (10 - 20 devs)
  - Complex domains with clear business capabilities
  - before transitioning to microservices

  **Famouse Examples**
  - Shopify (transitioned from this to microservices)
  - Many enterprise Java apps using Spring Modulith

  1.3 Microservices Architecture

  An architecture where the application is composed of small indepedent services, each running in its own process and communicating via lightweight protocols (HTTP/REST, gRPC, or message queues).

  **Structure**
                   [API Gateway]
                       │
    ┌──────────────────┼──────────────────┐
    │                  │                  │
User-Service    Payment-Service   Inventory-Service
    │                  │                  │
 [User DB]         [Payment DB]     [Inventory DB]
 (Each service has its OWN database)

 **charactersitics**
 - Each service has a single business capability
 - Independently deployable and scalable
 - Each service owns its own database
 - Polygot - different services can use different tech stacks
 - Communicate via APIs (synchronous) or events (asynchronous)

 **Pros**
 - Independent deployment - Update one service without redeplouing others
 - Scalability - scale only the services that need it
 - Team autonomy - Small teams own their services, ship faster
 - Fault isolation- One service crashing doesn't take down the whole system
 - Tech diversity - Use the best language/tool for each job
 - easier to rewrite - Replace one service without affecting others

 **Cons**
 - Distributed complexity - Nextwork latency, retries, timeouts
 - Data consistency - No ACIT trasactions, must use eventual consistency (Sage pattern)
 - DevOps overhead - Need kubernetes, service discovery, API gateways, centralized logging
 - Debugging nightmares - Tracing a request across 10 service is hard
 - Distributed monolith trap- If services call each other in chains, you lose independence
 - Expensive - More services = more infrasturcture costs

 **When to use**
 - Large teams : more than 20 devs
 - High-traffic application with different scaling needs
 - Organizations with mature DevOps culture
 - Products that need frequent, independent releases

 **Famous Example**
 - Netflix, Amazon, Uber Spotify


 1.4 Serverless / Functions-As-a-service (Faas)
 you write single purpose functiosn that are triggered by events and run in stateless containers managed entirely by a cloud provider. The cloud provider handles scaling, patching and infrastructure.

 **Structure**
 [Frontend] → [API Gateway]
                  │
    ┌─────────────┼─────────────┐
    │             │             │
resizeImage()  sendEmail()  processPayment()
    │             │             │
 [S3 Bucket]   [SES/SMTP]   [Stripe API]
 (Each function runs, does ONE thing, then shuts down)

 **Characteristics**
 - No servers to manage (infrastucture is abstracted)
 - Billed per execution (milliseconds of compute time)
 - Auto-scales from 0 to infinite instantly
 - Stateless - no presistent memory between invocations
 - Event-driven triggers (HTTP, file uploads, database changes, queues)

 **Pros**
 - Zero infrastructure management - No patching, no scaling configs
 - cost-effective- Pay only when your code runs
 - Infinite scalability - Handles traffic spikes automatically
 - Faster development - Focus only on business logic, not infrastructure


 **cons**
 - cold starts - function can take seconds to spin up if idle
 - stateless limitations - can't run long-running processes or keep memory state
 - vendor lock-in - tightly coupled to AWS/Azure/GCP
 - Debuggin is hard - Limited local testing capabilities
 - Execution limits - Most provider cap at 15 minutes max runtime

 **When to Use**
 - Inconsistent or sporadic(something happening at irregular times) workloads (file processing, webhooks)
 - Scheduled jobs (cron jobs)
 - Real-time file processing (Image resizing, video transcoding)
 - API endpoints with low traffic

 **Famouse Examples**
 - AWS lambda, Google cloud functions, Azure functions, Vercel, cloudfare workers



## Deployment System Architecture (Infrastructure)
- These define how servers, networks, and databases are physically organized.

2.1 Client-server Architecture
The most fundamental architecture where clients (browsers, mobile apps) request resources from a central server that processes requests and returns responses.

**Structure**
[Client/Browser]  ←→  [Single Server]  ←→  [Database]
     ↑                       ↑
  (User Device)    (Processes requests)

  **Charactersitics**
  - One server handles all application logic, authentication, bussines rules, and data access
  - clients are thin (just presentatoin)
  - centralized data management

  **Pros**
  - Simple - Easy to build, understand and deploy
  - cheap - one server, one database
  - secure - centralized control over data and access
  - Predictable - well understood model

  **Cons**
  - Single point of failure - server goes down, everything stops
  - Limited scaling - One server can only handle so much traffic
  - Monolithic by nature - hard to update without downtime

  **When to use**
  - Small projectes, prototypes, or internal tools
  - Apps with low user traffic
  - Educational projects


  2.2 TIER Architecture

  Separates the application into three logical/functional layers: Presentation, Application(Logic) and Data. Each tier runs on its own server.

  **Structure**
  [Client/Browser]  ←→  [Application Server]  ←→  [Database Server]
   (Tier 1)            (Tier 2)                   (Tier 3)
  (Presentation)       (Business Logic)          (Data Storage)


  **Characteristics**
  - Each tier is physically separate (different servers)
  - Presentation tier = frontend (React, Angular, HTML/Css)
  - Application tier = backend API (Nodejs, phython, java)
  - Data tier = database (PostgreSQL, MySQL, MongoDB)
  - Communication flows strictly downward: Client -> App -> DB


  **Pros**
  - separation of concerns - Each tier has a single responsibility
  - Scalability- Scale each tier independently 
  - Maintainability - Can update frontend without touching backend
  - Security - Database tier can be firewalled from direct public access


**Cons**
- More moving parts - Multiple servers to deploy , monitor and secure
- Network Latency - Each tier adds network hops
- Complexity - More configuration needed than client-server


**When to use**
- Most professinal web applications (basically the standard)
- Any app that needs to scale and be maintained over time

**Famouse Example**
- Almost every modern SaaS product (Notion, Slack , Stripe)

2.3 N-Tier/ Multi-Tier Architecture
An extension of 3-tier with additional layers for caching, load balancing, or middleware.


**structure**
[Client] → [Load Balancer] → [Web Server (Nginx)]
                                   ↓
                         [Application Server (Backend)]
                                   ↓
                           [Cache Layer (Redis)]
                                   ↓
                         [Database Server (Primary)]
                                   ↓
                         [Replica DB (Read-Only)]

**characteristics**
- Can have 4, 5, or more tiers
- Each tier adds a specific capability (caching, queuing, replication)
- Designed for high performance and resilience

**Pros**
- High performance - Caching reduces database pressure
- High availability – Load balancers and replicas prevent downtime
- Flexibility – Add or remove tiers as needed

**cons**
- Complex to manage – Many layers to deploy and debug
- Expensive – More servers = higher costs
- Latency – Each tier adds network delay (but caching offsets this)

**When to Use**
- High-traffic enterprise applications
- Apps requiring 99.99% uptime
- Systems with massive read/write loads

**Famouse Examples**
- E-commerce sites (Amazon), banking apps, social media platforms

3. ADVANCED & SPECIALIZED PATTERNS
These are used for massive scale, real-time data, or decentralized systems.

3.1 EVENT-DRIVEN ARCHITECTURE (EDA)

Components communicate by producting and consuming events through a message broker. Producers emit events ("UserSignedUp", "OrderPlaced"). Consumers react to these events asynchronously, without needing to know who produced them.

**Structure**
[Service A]  →  [Event Broker]  ←  [Service C]
                 (Kafka/RabbitMQ)    (Consumer)
                       ↑
[Service B]  →  (Publishes events)  →  [Service D]
   (Producer)                          (Consumer)


**Characteristics**
- Asynchronous communication (non-blocking)
- Loosely coupled – Services don't call each other directly
- Event schema shared between producers and consumers
- Often used with microservices to handle cross-service workflows

**pros**
- Extreme decoupling – Services don't know about each other
- Extreme decoupling – Services don't know about each other
- Scalability – Multiple consumers can process events in parallel
- Real-time processing – React to events as they happen

**cons**
- Complex debugging – Hard to trace a request across many events
- Eventual consistency – Hard to guarantee immediate data sync
- Message duplication – Requires idempotent consumers
- Broker management – Message brokers are complex to operate


**When to Use**
- Real-time systems (Uber ride matching, Twitter feed, IoT sensors)
- Systems where immediate response isn't critical (order confirmations, emails)
- When you need to notify multiple services about a single action


**Famous Examples**
- Kafka (LinkedIn), RabbitMQ, AWS SQS/SNS, Uber's dispatch system


3.2 SPACE-BASED ARCHITECTURE (Grid Computing)
 Processing and data are distributed across a grid of servers, with data stored entirely in memory (RAM) rather than disks. The "space" is a shared, in-memory data grid.

 **structure**
 [Load Balancer]
       │
┌──────┼──────┐
│      │      │
Node 1 Node 2 Node 3
(RAM)  (RAM)  (RAM)
(All nodes share the in-memory data grid)

**Characteristics**
- Data is stored in distributed RAM (e.g., Hazelcast, Redis Cluster)
- Processing happens on the same node where data lives (data affinity)
- No single database bottleneck
- Stateful (unlike stateless microservices)

**Pros**
- Blazing speed – RAM is thousands of times faster than disk
- Linear scalability – Add more nodes, get more processing power
- High availability – Data is replicated across nodes
- Handles spikes – Perfect for unpredictable traffic surges


**When to use**
- High-volume transactional systems (ticketing: Ticketmaster)
- Financial trading platforms
- Gaming leaderboards and session management
- Real-time analytics

**Famous Examples**
- Hazelcast, Apache Ignite, Oracle Coherence, Ticketmaster's booking system


3.3 PEER-TO-PEER (P2P) ARCHITECTURE
- No central server. Each node (peer) acts as both a client (requesting data) and a server (providing data). Nodes communicate directly with each other.

**structure**
   [Peer A] ←→ [Peer B]
      ↕          ↕
   [Peer C] ←→ [Peer D]
   (All peers are equal; no central authority)

   **Characteristics**
   - No central coordinator
   - Each peer is both a consumer and provider
   - Highly fault-tolerant (no single point of failure)
   - Requires discovery protocols to find other peers

   **Pros**
   - No infrastructure costs – Peers share the load
   - Extremely resilient – No central server to attack or crash
   - Censorship-resistant – Hard to shut down
   - Self-scaling – More users = more peers = more bandwidth


**cons**
- Security risks – Can't trust other peers
- Unreliable – Peers can leave anytime
- Complex protocol – Discovery, NAT traversal, and consensus are hard
- Latency – Data may come from across the world

**When to Use**

- Decentralized apps (Web3/Blockchain)
- File sharing (BitTorrent)
- Real-time video calling (WebRTC, where peers connect directly)
- Distributed ledgers (Bitcoin, Ethereum)

**famous example**
BitTorrent, Blockchain networks, WebRTC, IPFS




# decision flowchart
Start:
   ↓
Are you building a proof-of-concept/MVP?
   ↓
   YES → Use CLIENT-SERVER + MONOLITH (simplest)
   ↓
   NO → Is your team < 10 developers?
   ↓
   YES → Use 3-TIER + MODULAR MONOLITH (organized simplicity)
   ↓
   NO → Is your team 10–20 developers?
   ↓
   YES → Use 3-TIER + MODULAR MONOLITH (plan to split later)
   ↓
   NO → Is your team 20+ developers?
   ↓
   YES → Do you have a mature DevOps team with Kubernetes experience?
   ↓
   YES → Use MICROSERVICES (with API Gateway + Service Mesh)
   ↓
   NO → Stick with MODULAR MONOLITH (too early for microservices)
   ↓
Additional Filters:
   → Are your traffic patterns highly unpredictable/spiky? → Consider SERVERLESS
   → Do you need real-time async workflows? → Add EVENT-DRIVEN
   → Do you have massive transactional spikes (ticketing)? → Consider SPACE-BASED
   → Are you building a decentralized app? → Consider P2P

   # Gloden rule 
   Start with the simplest architecture that solves today's problem. Evolve to complexity only when the business demands it.
# Study Notes: Production Deployment Components

## Learning Objectives
By the end of this material, you should be able to:
- Describe components commonly required for deployment in a production environment
- Describe the purpose of a firewall and a load balancer
- Differentiate between different types of servers

---

## The Big Picture: An N-Tier Production Architecture

The video walks through a typical **n-tier architecture diagram** for deploying an application in production. Here's the layout, top to bottom:

```
┌─────────────────────────────────────┐
│  PRESENTATION TIER                    │  ← front-end client apps
├─────────────────────────────────────┤  ← FIREWALL (everything below is behind it)
│  WEB TIER                             │  ← web load balancer → web servers
├─────────────────────────────────────┤
│  APPLICATION SERVER TIER              │  ← app load balancer / proxy → app servers
├─────────────────────────────────────┤
│  DATA TIER                            │  ← database server (+ high-availability replica)
└─────────────────────────────────────┘
```

### Tier-by-Tier Breakdown

| Tier | Contains | Purpose |
|---|---|---|
| **Presentation tier** | Front-end client applications | What the end-user directly interacts with |
| *(Firewall sits here)* | — | Protects everything below it from outside threats |
| **Web tier** | Web load balancer + multiple web servers | Distributes and handles incoming web traffic |
| **Application server tier** | App load balancer/proxy server + application servers | Routes traffic, runs business logic |
| **Data tier** | Database server (+ high-availability replica) | Stores and manages data; replica ensures reliability |

> **Important caveat:** Not every deployment needs all of these. For example, some environments might not need **both** web servers and application servers — it depends on the system's needs.

---

## Key Components Explained

### 1. Firewall
**Definition:** A **security device** that monitors traffic **between networks**.

- Permits or blocks data based on a set of **security rules**
- Acts as a **barrier** between networks
- Blocks viruses, malware, and hackers from reaching the internal network

### 2. Load Balancer
**Purpose:** Distributes network traffic **efficiently** across multiple servers (a group of servers is called a **server farm**).

- Sits **between clients and servers**
- Prevents any single server from being **overloaded**
- Decides which servers can best fulfill incoming requests → maximizes **availability** and **responsiveness**
- Manages concurrent client requests, returning data quickly and reliably

> **Two load balancers appear in the diagram:** a **web load balancer** (web tier) and an **app load balancer** (application server tier) — each distributing traffic within its own tier.

### 3. Web Servers
**Definition:** Software or machines that deliver **content** — web pages, files, images, videos — to a client.

- Primarily responds to **HTTP requests** (e.g., a user's browser accessing a website)
- Falls under the general category of "servers": software/machines providing services, resources, data, or applications to a client

### 4. Application (App) Servers
**Definition:** Runs the **business logic** and provides the application to the client — instead of the client running the app locally on their own machine.

- Enables interaction between the **end-user** and the **server-side application code**
- The business logic determines:
  - How data is created, stored, and changed
  - Transaction results
  - What data is written to / retrieved from a database

> **Web server vs. App server, in short:** Web servers deliver *content*; app servers run the *business logic*.

### 5. Proxy Server
**Definition:** An **intermediate server** that sits between two tiers and handles requests passing between them.

Can serve **multiple purposes**:
- Load balancing
- System optimization
- Caching
- Acting as a firewall
- Obscuring the source of a request (privacy)
- Encryption
- Scanning for malware

> A proxy server improves the **efficiency, privacy, and security** of data flowing through a network.

### 6. Database & Database Server
- **Database:** A collection of related data stored on a computer, accessible in various ways
- **DBMS (Database Management System):** The software that controls a database and connects it to users/other programs
- **Database server:** Controls the **flow and storage** of data
- The DBMS is what lets an **application** retrieve or manipulate the data stored in the database

---

## Summary Comparison Table

| Component | Type | Main Job |
|---|---|---|
| **Firewall** | Security device | Monitor & filter traffic between networks |
| **Load Balancer** | Traffic manager | Distribute requests across a server farm |
| **Web Server** | Server | Deliver content (pages, files, images, video) via HTTP |
| **App Server** | Server | Run business logic, serve the application itself |
| **Proxy Server** | Intermediate server | Handle/optimize/secure requests between tiers |
| **Database Server** | Server | Store & control the flow of data (via a DBMS) |

---

## Quick Recap / Summary

- A production deployment is often organized as an **n-tier architecture**: presentation → web → application → data, with a **firewall** protecting everything past the presentation tier
- **Firewall**: security barrier that filters traffic between networks
- **Load balancer**: spreads traffic across multiple servers so none gets overloaded
- **Web server**: delivers content, responds to HTTP requests
- **App server**: runs business logic, serves the application to the client
- **Proxy server**: sits between tiers, can load balance, cache, secure, encrypt, and more
- **Database server**: stores/manages data via a DBMS, which connects the database to the application
- Not all components are required in every deployment — it depends on the system

---

## Self-Check Questions
Use these to test your recall before moving on:

1. Draw or describe the n-tier production architecture from top to bottom, including where the firewall sits.
2. What's the difference between a web server and an application server?
3. What is a "server farm," and what problem does a load balancer solve for it?
4. List at least four different purposes a proxy server can serve.
5. What is the role of a DBMS, and how does it relate to a database server?
6. Why might a high-availability replica be used in the data tier?
7. Give a scenario where a deployment might not need both web servers and app servers.

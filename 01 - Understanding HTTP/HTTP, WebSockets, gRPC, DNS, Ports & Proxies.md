

> [!abstract] Overview  
> These are the fundamental concepts behind how **clients, servers, networks, APIs, and backend applications communicate**.
> 
> ==Understanding these concepts is essential for backend engineering and system design interviews.==

---

# 1. HTTP — HyperText Transfer Protocol

## What is HTTP?

**HTTP** stands for **HyperText Transfer Protocol**.

It is a protocol used for communication between a **client** and a **server**.

> [!important]  
> ==HTTP follows a request → response communication model.==

### Basic HTTP Flow

```text
┌───────────────┐
│ Browser       │
│ Client        │
└───────┬───────┘
        │
        │ HTTP Request
        ↓
┌───────────────┐
│ Backend       │
│ Server        │
└───────┬───────┘
        │
        │ HTTP Response
        ↓
┌───────────────┐
│ Browser       │
│ Client        │
└───────────────┘
```

## HTTP Communication Pattern

```text
Client  →  Server
          Request

Client  ←  Server
          Response
```

### Important Characteristics

- **Client** sends a request.
    
- **Server** processes the request.
    
- **Server** sends a response.
    
- HTTP is fundamentally **stateless**.
    
- Modern HTTP versions can use **persistent connections**.
    

> [!warning] Common Misconception  
> Do not say:
> 
> =="HTTP always closes the connection after every response."==
> 
> Modern **HTTP/1.1** and **HTTP/2** can reuse persistent connections.

---

# 2. WebSockets

## What are WebSockets?

**WebSockets** provide a **persistent, two-way communication channel** between the client and server.

Unlike the traditional HTTP request-response model, once a WebSocket connection is established:

> [!important]  
> ==Both the client and server can send messages at any time.==

## WebSocket Flow

```text
┌───────────────┐
│    Client     │
└───────┬───────┘
        │
        │ Connect
        ↓
┌───────────────┐
│    Server     │
└───────┬───────┘
        │
        │
        │  Persistent Connection
        │
        │
        ↕
   Client ↔ Server
   Both communicate
      anytime
        │
        │ Disconnect
        ↓
 Connection Closed
```

## Where are WebSockets Used?

WebSockets are useful when an application needs **real-time communication**.

Examples:

- 💬 Chat applications
    
- 🔔 Live notifications
    
- 🎮 Online gaming
    
- 📈 Live stock prices
    
- 📊 Real-time dashboards
    

## HTTP vs WebSockets

|HTTP|WebSockets|
|---|---|
|Mainly request-response|Two-way communication|
|Client usually initiates communication|Both sides can initiate messages|
|Commonly used for REST APIs|Commonly used for real-time applications|
|Connections can be reused|Persistent connection|
|Example: Fetch user details|Example: Chat application|

> [!tip] Interview Shortcut  
> **HTTP → Request/Response**
> 
> **WebSocket → Persistent + Two-way communication**

---

# 3. gRPC

## What is gRPC?

**gRPC** stands for **Google Remote Procedure Call**.

It is a **high-performance RPC framework** originally developed at Google for communication between services.

> [!important]  
> ==gRPC is commonly used for service-to-service communication in distributed systems and microservices.==

## How gRPC Works

Instead of manually sending JSON over HTTP APIs, gRPC commonly uses:

- **Protocol Buffers (Protobuf)** for serialization
    
- **HTTP/2** for transport
    

### REST-style Communication

```text
Client
   │
   │ HTTP
   ↓
 JSON
   │
   ↓
Server
```

### gRPC Communication

```text
Client
   │
   │ HTTP/2
   ↓
Protobuf
   │
   ↓
Server
```

### JSON Example

```json
{
  "userId": 101,
  "name": "Goushik"
}
```

gRPC commonly uses **Protobuf**, which represents the same information in a compact binary format.

At the machine level, binary data is represented using bits:

```text
01010101...
```

> [!note]  
> The important idea is not the `01010101` itself.
> 
> ==Protobuf provides a compact binary serialization format that can make service communication efficient.==

## gRPC in Microservices

Imagine a system with multiple services:

```text
                  ┌─────────────────┐
                  │   User Service  │
                  └────────┬────────┘
                           │
                           ↓
                  ┌─────────────────┐
                  │ Payment Service │
                  └────────┬────────┘
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
      Notification    Movie Service   Recommendation
         Service                        Service
```

These internal services can communicate with each other using **gRPC**.

## Key Point

```text
REST API
Client → HTTP → JSON → Server

gRPC
Client → HTTP/2 → Protobuf → Server
```

> [!important] Remember  
> ==gRPC commonly uses HTTP/2 + Protocol Buffers.==

---

# 4. DNS — Domain Name System

## What is DNS?

**DNS** stands for **Domain Name System**.

DNS translates a **human-readable domain name** into an **IP address** that computers can use to locate a server.

> [!tip] Easy Analogy  
> ==DNS is like the phone book of the Internet.==

## Example

```text
google.com
     │
     ↓
    DNS
     │
     ↓
 IP Address
```

For example:

```text
google.com → 142.250.x.x
```

> [!warning]  
> IP addresses can change.
> 
> Therefore, don't treat a particular IP address as permanently belonging to a domain.

## DNS Flow

```text
┌───────────────┐
│    Browser    │
└───────┬───────┘
        │
        │ "What is the IP address
        │  of Amazon.com?"
        ↓
┌───────────────┐
│      DNS      │
└───────┬───────┘
        │
        │ IP Address
        ↓
   54.xxx.xxx.xxx
        │
        │ HTTP Request
        ↓
┌───────────────┐
│ Amazon Server │
└───────┬───────┘
        │
        │ HTTP Response
        ↓
      Browser
```

## Why Do We Need DNS?

Humans prefer domain names:

```text
google.com
amazon.com
youtube.com
```

Computers communicate using IP addresses such as:

```text
142.250.x.x
```

Therefore:

> [!important]  
> ==DNS connects human-readable domain names with IP addresses.==

---

# 5. IP Address

## What is an IP Address?

An **IP (Internet Protocol) address** is an address used to identify and communicate with a **device/network interface on a network**.

Example:

```text
192.168.1.10
```

### Simple Analogy

```text
IP Address = Building Address
```

However, one computer can run many different services or applications.

This is where **ports** become important.

> [!important]  
> ==IP address identifies the network destination; the port identifies the service on that destination.==

---

# 6. Port

## What is a Port?

A **port** identifies a particular **network service/application** running on a machine.

### Easy Analogy

```text
IP Address = Building Address
Port        = Apartment / Door Number
```

## Example

```text
Computer
IP Address: 192.168.1.10

        │
        ├── Port 22   → SSH
        ├── Port 80   → HTTP
        ├── Port 443  → HTTPS
        ├── Port 3306 → MySQL
        ├── Port 5432 → PostgreSQL
        └── Port 6379 → Redis
```

## Common Ports

|Port|Service|
|--:|---|
|**22**|SSH|
|**80**|HTTP|
|**443**|HTTPS|
|**3306**|MySQL|
|**5432**|PostgreSQL|
|**6379**|Redis|

## IP + Port

Suppose:

```text
IP Address = 192.168.1.10
```

The IP tells us **which network destination** we want to communicate with.

The port tells us **which service** we want to reach.

Example:

```text
192.168.1.10:5432
```

means:

> [!important]  
> Connect to the **PostgreSQL service** at **port 5432** on that machine.

### Interview Shortcut

```text
IP Address → Where?
Port        → Which service?
```

---

# 7. Proxy

## What is a Proxy?

A **proxy** is an intermediary between two parties.

Instead of communicating directly with the destination, the request goes through the proxy.

```text
Client → Proxy → Server
```

There are two important types:

1. **Forward Proxy**
    
2. **Reverse Proxy**
    

---

# 8. Forward Proxy

## What is a Forward Proxy?

A **forward proxy** sits between the **client and the Internet**.

```text
┌──────────┐
│   You    │
└────┬─────┘
     ↓
┌─────────────────┐
│ Forward Proxy   │
└────┬────────────┘
     ↓
┌─────────────────┐
│    Internet     │
└────┬────────────┘
     ↓
┌──────────┐
│  Google  │
└──────────┘
```

The client sends the request to the proxy, and the proxy communicates with the destination server.

## Example: Company Network

```text
Employee
   │
   ↓
Company Proxy Server
   │
   ↓
Internet
   │
   ↓
Google
```

A company may use a forward proxy to:

- Block websites
    
- Monitor Internet usage
    
- Cache frequently accessed resources
    
- Apply access policies
    
- Hide the client's IP from the destination in some setups
    

### Simple Analogy

> **You → Receptionist → Outside World**

The receptionist communicates with the outside world on your behalf.

> [!important] Remember  
> ==Forward Proxy → Represents/serves the client side.==

---

# 9. Reverse Proxy

## What is a Reverse Proxy?

A **reverse proxy** sits in front of the **server/application**.

```text
Client
   │
   ↓
Reverse Proxy
   │
   ↓
Backend Server
```

A common example is **Nginx**.

## Without Reverse Proxy

```text
Browser
   │
   ↓
Node.js :3000
   │
   ↓
Database
```

The client directly communicates with the Node.js application.

## With Reverse Proxy

```text
Browser
   │
   ↓
Nginx
   │
   ↓
Node.js
   │
   ↓
Database
```

The browser communicates with **Nginx**, and Nginx forwards the request to the appropriate backend service.

## What Can a Reverse Proxy Do?

A reverse proxy can provide:

- **Request routing**
    
- **Load balancing**
    
- **SSL/TLS termination**
    
- **Security controls**
    
- **Caching**
    
- **Compression**
    
- **Hiding backend server details**
    

### Simple Analogy

Imagine a hotel:

```text
Customer
   │
   ↓
Receptionist
   │
   ↓
Room 201
```

The customer doesn't directly walk into the restricted room.

The receptionist can:

- Check whether the guest is allowed
    
- Perform security checks
    
- Determine which room/service should receive the request
    
- Forward the guest appropriately
    

Similarly:

```text
Client
   │
   ↓
Reverse Proxy
   │
   ↓
Backend Server
```

> [!important] Interview Shortcut  
> **Forward Proxy → Client side**
> 
> **Reverse Proxy → Server side**

---

# 10. HTTP Statelessness

## What Does Stateless Mean?

HTTP is fundamentally a **stateless protocol**.

> [!important]  
> ==Stateless means the server does not inherently remember the state of previous requests at the HTTP protocol level.==

Each request contains the information necessary for the server to process that request.

## Example

### Request 1

```text
Client → Server

"Give me user 101"
```

### Response

```text
Client ← Server

"Here is user 101"
```

Later:

### Request 2

```text
Client → Server

"Give me user 102"
```

The second request is treated independently at the **HTTP protocol level**.

## Does Stateless Mean the Application Cannot Remember Users?

**No.**

This is an important distinction.

Applications can maintain state using mechanisms such as:

- **Cookies**
    
- **Sessions**
    
- **JWTs**
    
- **Databases**
    
- **Caches**
    

Therefore:

```text
HTTP
  ↓
Stateless by design

Application
  ↓
Can maintain state using additional mechanisms
```

> [!warning] Interview Trap  
> **Stateless ≠ The application cannot store user information.**
> 
> It means HTTP itself does not inherently maintain the state of previous requests.

---

# 11. Client-Server Model

## What is the Client-Server Model?

The **client-server model** is an architecture in which:

1. The **client** requests a service/resource.
    
2. The **server** processes the request.
    
3. The **server** sends a response.
    

### Basic Flow

```text
┌───────────────┐
│    Client     │
└───────┬───────┘
        │
        │ Request
        ↓
┌───────────────┐
│    Server     │
└───────┬───────┘
        │
        │ Response
        ↓
┌───────────────┐
│    Client     │
└───────────────┘
```

---

## Who is the Client?

A **client** is a program, device, or service that makes a request to another service.

Examples:

- **Chrome browser**
    
- **Mobile application**
    
- **Postman**
    
- **Another backend service**
    
- **Frontend application**
    

### Example

When you open a website:

```text
Chrome
   │
   │ HTTP Request
   ↓
Web Server
```

Chrome acts as the **client**.

---

# 12. Who is the Server?

A **server** is a program that:

1. **Listens** for incoming requests
    
2. **Processes** those requests
    
3. **Sends** responses
    

## Express Example

```typescript
app.listen(3000);
```

This starts the Express application listening for incoming network connections on port `3000`.

Therefore:

> [!important]  
> ==The Express application is acting as a server.==

### Flow

```text
Client
   │
   │ Request
   ↓
Express Server :3000
   │
   │ Response
   ↓
Client
```

---

# 13. Complete Client-Server Request Flow

When you access a website, a simplified flow can look like this:

```text
┌───────────────┐
│    Browser    │
└───────┬───────┘
        │
        ↓
┌───────────────┐
│      DNS      │
└───────┬───────┘
        │
        │ Find IP Address
        ↓
┌───────────────────┐
│ HTTP / HTTPS      │
│ Request           │
└─────────┬─────────┘
          │
          ↓
┌───────────────────┐
│       Nginx       │
│ Reverse Proxy     │
└─────────┬─────────┘
          │
          ↓
┌───────────────────┐
│      Node.js      │
│ Backend           │
└─────────┬─────────┘
          │
          ↓
┌───────────────────┐
│     Database      │
└─────────┬─────────┘
          │
          ↓
┌───────────────────┐
│      Node.js      │
└─────────┬─────────┘
          │
          ↓
┌───────────────────┐
│       Nginx       │
└─────────┬─────────┘
          │
          ↓
┌───────────────┐
│    Browser    │
└───────────────┘
```

## Step-by-Step

### 1. Browser

The user enters:

```text
https://example.com
```

### 2. DNS

DNS resolves the domain name to an IP address.

```text
example.com
     ↓
IP Address
```

### 3. Browser Sends the Request

The browser sends an **HTTP/HTTPS request** to the server.

### 4. Nginx Receives the Request

Nginx acts as a **reverse proxy** and can route the request to the appropriate backend.

### 5. Node.js Processes the Request

The Node.js application handles the **business logic**.

### 6. Database

If required, Node.js communicates with the database.

### 7. Response

The response travels back:

```text
Database
   ↓
Node.js
   ↓
Nginx
   ↓
Browser
```

> [!important] Big Picture  
> ==DNS helps find the destination → HTTP/HTTPS carries the request → Reverse proxy routes it → Backend processes it → Database provides data → Response travels back to the client.==

---

# Quick Revision

> [!tip] 🚀 One-Minute Revision

```text
HTTP
→ Communication protocol between client and server
→ Request / Response
→ Stateless at protocol level

WebSocket
→ Persistent connection
→ Two-way communication
→ Real-time applications

gRPC
→ High-performance RPC framework
→ Commonly uses HTTP/2
→ Uses Protocol Buffers

DNS
→ Domain Name System
→ Domain name → IP address

IP Address
→ Identifies a network destination/interface

Port
→ Identifies a service on a machine

Forward Proxy
→ Sits between client and Internet
→ Represents client side

Reverse Proxy
→ Sits in front of backend servers
→ Represents server side

Client
→ Makes the request

Server
→ Processes the request
→ Sends the response
```

---

# ⭐ Interview Cheat Sheet

|Concept|Remember This|
|---|---|
|**HTTP**|Request → Response|
|**WebSocket**|Persistent + Two-way|
|**gRPC**|HTTP/2 + Protobuf|
|**DNS**|Domain → IP|
|**IP Address**|Network destination|
|**Port**|Service on destination|
|**Forward Proxy**|Client side|
|**Reverse Proxy**|Server side|
|**Stateless HTTP**|Previous request state isn't inherently maintained by HTTP|
|**Client**|Sends request|
|**Server**|Processes request + sends response|

> [!important] 🔥 Most Important Connections
> 
> ```text
> Domain Name
>      ↓
>     DNS
>      ↓
>  IP Address
>      ↓
>     Port
>      ↓
>   Service
>      ↓
> HTTP / HTTPS
>      ↓
> Reverse Proxy
>      ↓
> Backend Server
>      ↓
> Database
> ```
> 
> ==This is the mental model you should remember when thinking about how a backend request travels through a system.==
> 


Persistent connection:

 - A persisten connection means the TCP connection stays open even after the first request, So multiple HTTP request can use the same connection
   
Instead 
- connect -> request -> response -> Disconnect
  
It became:
- connect -> req 1 -> res 1 -> req 2 -> res 2 -> req 3 -> res 3 -> disconnect
  

What is multplexing

- It means multiple http server and response can travel one the same TCP connection simultaneously
  

Browser -> req1,res2,res3 -> all at once(server process) -> response return independently

Types of HTTP headers:

- An Http is a meta data (Information) about a request and response
  
  
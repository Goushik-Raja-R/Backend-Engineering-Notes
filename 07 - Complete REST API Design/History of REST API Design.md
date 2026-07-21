
## 🌐 The Beginning of the World Wide Web (WWW)

### 1989–1990 : Tim Berners-Lee

> [!info] Overview
> Tim Berners-Lee proposed the **World Wide Web (WWW)** at **CERN** to help researchers share and access information easily over the Internet.

His vision was to create a system where documents could be linked together and accessed from anywhere in the world.

---

# Technologies Invented by Tim Berners-Lee

Within a year, Tim developed the core technologies that formed the foundation of the Web.

## 1. URI (Uniform Resource Identifier)

- Gives every resource on the web a unique address.
- Example

```text
https://www.amazon.com/products/101
```

---

## 2. HTTP (HyperText Transfer Protocol)

- Communication protocol between Client and Server.
- Used to send Requests and Responses.

---

## 3. HTML (HyperText Markup Language)

- Standard language used to create web pages.

---

## 4. First Web Server

- Served web pages to clients.
- Hosted the first website.

---

## 5. First Web Browser

- Named **WorldWideWeb** (later renamed **Nexus**).
- Used to view and edit web pages.

---

## 6. WYSIWYG (What You See Is What You Get)

- Allowed users to edit documents visually.
- Users could see the final output while editing.

---

# Growth of the Web

As the World Wide Web became popular, millions of users and websites started using it.

This rapid growth created new challenges:

- Scalability
- Maintainability
- Performance
- Standardization
- Communication between distributed systems

A better architectural style was needed to support the growing Web.

---

# Roy Fielding and REST

## 2000 : Roy Fielding

> [!info]
> Roy Fielding introduced **REST (Representational State Transfer)** in his PhD dissertation.

REST is **not a protocol**.

REST is an **Architectural Style** for designing scalable web applications and APIs.

Its purpose is to make distributed systems simple, scalable, maintainable, and efficient.

---

# REST Architectural Constraints

REST is based on six architectural constraints.

## 1. Client-Server

- Separates the User Interface from Business Logic.
- Client handles presentation.
- Server handles data and business logic.

---

## 2. Stateless

- Every request is independent.
- The server does not remember previous requests.
- Every request must contain all the required information.

---

## 3. Cacheable

- Responses should indicate whether they can be cached.
- Reduces unnecessary server requests.
- Improves performance.

---

## 4. Uniform Interface

- Standard way of communicating between Client and Server.
- Makes APIs consistent and easier to understand.

---

## 5. Layered System

- A client does not know whether it is communicating directly with the server or through intermediaries like API Gateways, Load Balancers, or Proxies.

---

## 6. Code on Demand (Optional)

- Server can send executable code to the client when required.
- Example: JavaScript downloaded by the browser.

> [!note]
> This is the **only optional REST constraint**.

---

# HTTP 1.1

As the Web continued to grow, HTTP required improvements.

Roy Fielding was one of the key authors of the **HTTP/1.1** specification, which standardized and improved HTTP for large-scale web applications.

---

# Timeline

```text
1989
│
├── Tim Berners-Lee proposes the World Wide Web (WWW)
│
1990
│
├── URI
├── HTTP
├── HTML
├── First Web Server
├── First Web Browser
│
1993–1999
│
├── Rapid growth of the Web
├── Scalability challenges
│
2000
│
├── Roy Fielding publishes his PhD dissertation
├── Introduces REST
├── Defines REST Architectural Constraints
```

---

# REST vs HTTP

| REST | HTTP |
|------|------|
| Architectural Style | Communication Protocol |
| Defines how APIs should be designed | Defines how Client and Server communicate |
| Focuses on scalability and maintainability | Focuses on transferring data |

---

# Why REST Was Introduced?

REST was introduced to:

- Improve scalability
- Standardize communication
- Simplify distributed systems
- Improve maintainability
- Support the rapid growth of the Web

---

# Key Points

> [!tip]

- Tim Berners-Lee invented the World Wide Web (WWW).
- He introduced URI, HTTP, HTML, the first Web Server, and the first Web Browser.
- As the Web grew, better architectural principles were needed.
- Roy Fielding introduced REST in his PhD dissertation.
- REST is an **Architectural Style**, not a protocol.
- HTTP is the communication protocol commonly used to implement REST APIs.
- REST is based on six architectural constraints, with **Code on Demand** being optional.

---

# One-Line Revision

> **Tim Berners-Lee created the World Wide Web, and Roy Fielding introduced REST to define an architectural style for building scalable, maintainable web systems.**
# JSON Web Token (JWT)

### Why JWT?

As modern applications became distributed across multiple servers and microservices, maintaining server-side sessions became difficult. JWT provides a **stateless authentication mechanism**, allowing each request to carry its own authentication information without storing session data on the server.

---

### Stateless

> **Stateless means the server does not store client session information. Every request is independent and contains all the information required for authentication.**

---

### JWT Structure

```
Header.Payload.Signature
```

Example

```
eyJhbGciOiJIUzI1NiIs...
```

---

### 1. Header

Stores metadata about the token.

Contains:

- Token type (JWT)
- Signing algorithm (HS256, RS256)

Example

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

---

### 2. Payload

Stores **claims** (information about the user).

Examples

- User ID
- Email
- Role
- Issued At (`iat`)
- Expiration Time (`exp`)

Example

```
{
  "userId":101,
  "role":"Admin",
  "iat":1719823000,
  "exp":1719826600
}
```

---

### 3. Signature

Generated using:

```
Header + Payload + Secret Key
```

Purpose:

- Verifies the token was issued by a trusted server.
- Detects if the token has been modified.

---

### JWT Authentication Flow

```
User Login
      │
      ▼
Server verifies credentials
      │
      ▼
Creates JWT
      │
      ▼
JWT sent to Browser
      │
      ▼
Browser stores JWT
      │
      ▼
Every request sends JWT
      │
      ▼
Server verifies Signature
      │
      ▼
Access Granted
```

# Stateless

## Definition
> Stateless means the server does not store any client session information. Every request is independent and contains all the information required to process it.

## Characteristics
- Server does not remember previous requests.
- Every request is treated as a new request.
- Authentication data (JWT) is sent with every request.
- No server-side session storage is required.

## Example
```text
Client
   │
   ├── Request 1 + JWT
   ├── Request 2 + JWT
   └── Request 3 + JWT

Server verifies the JWT for every request.
```

---

# Scalability

## Definition
> Scalability is the ability of a system to handle increasing users or workload by efficiently adding more resources.

## Characteristics
- Supports more users without affecting performance.
- Multiple servers can handle requests.
- Load balancers distribute requests among servers.
- JWT improves scalability because no session lookup is required.

## Example
```text
           Load Balancer
           /     |     \
          /      |      \
     Server A  Server B  Server C
```

---

# Portability

## Definition
> Portability is the ability to use the same JWT across multiple servers, services, or platforms without depending on a specific server.

## Characteristics
- Same JWT works across different servers.
- Ideal for distributed systems and microservices.
- No need to create separate sessions on each server.

## Example
```text
Browser
   │
   ▼
JWT
   │
   ├── User Service
   ├── Order Service
   ├── Payment Service
   └── Notification Service
```

---

# Quick Comparison

| Concept | Meaning |
|----------|---------|
| **Stateless** | Server stores no client session; every request is independent. |
| **Scalability** | Ability of a system to handle more users by adding resources. |
| **Portability** | Same JWT can be used across multiple servers and services. |

---

# Memory Trick

- **Stateless** → Server remembers nothing.
- **Scalability** → System grows easily.
- **Portability** → Same JWT works everywhere.
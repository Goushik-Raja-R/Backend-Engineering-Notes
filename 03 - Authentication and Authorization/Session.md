
## Definition

> A **session** is a server-side mechanism used to maintain a user's authenticated state across multiple HTTP requests.

---

# Why do we need Sessions?

HTTP is **stateless**, meaning the server does not remember previous requests.

A session helps the server remember a logged-in user without requiring them to log in again for every request.

---

# How Session Works

```text
User Login
     │
     ▼
Server verifies credentials
     │
     ▼
Creates a Session
     │
     ▼
Generates a unique Session ID
     │
     ▼
Stores Session Data
(Memory / Redis / Database)
     │
     ▼
Sends Session ID to Browser Cookie
     │
     ▼
Every Request
     │
     ▼
Browser automatically sends Session ID
     │
     ▼
Server retrieves Session Data
     │
     ▼
User Authenticated
```

---

# Where is Session Stored?

### Browser

Stores only the **Session ID** inside a Cookie.

```text
Cookie

sessionId = abc123xyz
```

### Server

Stores the actual session information.

```text
Session ID : abc123xyz

↓

{
    userId : 101,
    username : "Goushik",
    role : "User"
}
```

---

# Session Storage Options

## 1. Memory Store

- Stores sessions in the application's RAM.
- Very fast.
- Sessions are lost when the server restarts.
- Suitable only for development.

---

## 2. Redis

- Stores sessions in Redis memory (RAM).
- Extremely fast.
- Shared across multiple application servers.
- Recommended for production environments.

---

## 3. Database

- Stores sessions in MySQL, PostgreSQL, MongoDB, etc.
- Persistent.
- Slower than Redis.
- Less commonly used for session storage.

---

# Advantages

- Maintains user login state.
- Easy to implement.
- Easy to invalidate sessions (logout).
- Sensitive user data remains on the server.

---

# Disadvantages

- Requires server-side storage.
- Consumes server memory.
- Needs Redis or another shared store to scale across multiple servers.

---

# Session vs JWT

| Session | JWT |
|----------|-----|
| Stateful | Stateless |
| Stores user data on the server | Stores user information inside the token |
| Requires Session Store | No Session Store required |
| Browser stores Session ID | Browser stores JWT |
| Easy to revoke | Revocation requires additional mechanisms |

---

# Interview Questions

### What is a Session?

> A session is a server-side mechanism that stores user-specific information after authentication, allowing the server to recognize the user across multiple HTTP requests.

---

### Why do we need Sessions?

> Because HTTP is stateless, sessions help maintain a user's authenticated state across multiple requests.

---

### Where is the Session stored?

- **Session ID** → Browser Cookie
- **Session Data** → Server (Memory, Redis, Database)

---

### Is Session Stateful?

> Yes. The server stores information about the user's session.

---

### Why is Redis preferred for Session Storage?

> Redis is an in-memory data store that is fast, scalable, and allows multiple application servers to share the same session data.

---

# Memory Trick

## Hotel Analogy

```text
Guest arrives
      │
      ▼
Reception verifies identity
      │
      ▼
Creates Guest Record
      │
      ▼
Issues Room Key
      │
      ▼
Guest requests a service
      │
      ▼
Shows Room Key
      │
      ▼
Reception finds Guest Record
      │
      ▼
Provides Service
```

- **Room Key** → Session ID
- **Guest Record** → Session Data
- **Reception** → Server

---

# One-Line Notes

- **Session:** A server-side mechanism that maintains a user's authenticated state across multiple HTTP requests.
- **Session ID:** A unique identifier stored in the browser cookie that references the user's session on the server.
- **Session Store:** The location where session data is stored (Memory, Redis, or Database).
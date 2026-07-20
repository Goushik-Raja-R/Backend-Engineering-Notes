

> [!info] Definition
> Logging & Monitoring Middleware records details about every request and response to help with debugging, monitoring, and auditing.

---

# Purpose

- Record API requests
- Measure response time
- Detect errors
- Monitor application performance

---

# Common Information Logged

- HTTP Method
- URL
- Status Code
- Response Time
- Timestamp
- Client IP

---

# Example Log

```text
GET /users
Status: 200
Response Time: 35 ms
```

---

# How It Works

Client
│
▼
HTTP Request
│
▼
Logging Middleware
│
▼
Store Log Information
│
▼
Controller

---

# Real-Life Example

Think of a CCTV camera.

It doesn't stop people from entering.

It simply records everything happening.

Logging Middleware behaves the same way by recording every request.

---

# Popular Packages

- Morgan
- Winston
- Pino

---

# Advantages

- Easier debugging
- Performance monitoring
- Audit trails
- Error investigation

---

# One-Line Note

> Logging Middleware records request and response details for monitoring and debugging.
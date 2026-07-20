

> [!info] Definition
> Security Middleware protects the application by verifying that incoming requests are legitimate and preventing unauthorized access or common security attacks.

---

# Purpose

- Authenticate users
- Authorize users
- Protect APIs
- Prevent common web attacks
- Ensure only trusted requests reach the Controller

---

# Common Examples

- JWT Authentication
- Session Authentication
- API Key Validation
- CORS
- Helmet
- Rate Limiting
- CSRF Protection

---

# How It Works

Client
│
▼
HTTP Request
│
▼
Security Middleware
│
├── Valid Request
│       │
│       ▼
│   Controller
│
└── Invalid Request
        │
        ▼
401 Unauthorized / 403 Forbidden

---

# Real-Life Example

Imagine entering a company office.

A security guard checks your ID card before allowing you inside.

- Valid ID → Entry Allowed
- Invalid ID → Entry Denied

The security guard is the **Security Middleware**.

---

# Advantages

- Prevents unauthorized access
- Protects sensitive APIs
- Improves application security
- Stops malicious requests early

---

# One-Line Note

> Security Middleware verifies whether a request is trusted before allowing it to reach the Controller.
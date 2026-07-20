
## Definition

> An **API Key** is a unique secret identifier used to authenticate and identify an application or client when accessing an API.

---

# Why do we need API Keys?

API Keys are used to:

- Authenticate an application.
- Control access to APIs.
- Track API usage.
- Apply rate limiting.
- Prevent unauthorized access.

---

# How API Key Works

```text
Client Application
        │
        ▼
Attach API Key
        │
        ▼
HTTP Request
        │
        ▼
API Server
        │
        ▼
Validate API Key
        │
   ┌────┴────┐
   │         │
Valid     Invalid
   │         │
Response   401/403
```

---

# Authentication Flow

```text
Developer
     │
     ▼
Registers Application
     │
     ▼
API Provider Generates API Key
     │
     ▼
Stores API Key in Backend (.env)
     │
     ▼
Backend Sends API Key with Every API Request
     │
     ▼
API Server Verifies API Key
     │
     ▼
Access Granted
```

---

# Where is API Key Stored?

✅ Backend

```text
.env

OPENAI_API_KEY=sk-xxxxxxxx
```

❌ Never store in:

- React
- Angular
- Vue
- Mobile Apps (unless using platform-specific secure storage with appropriate restrictions)
- Public GitHub repositories

---

# Where is API Key Sent?

### Authorization Header

```http
Authorization: Bearer <API_KEY>
```

### Custom Header

```http
x-api-key: <API_KEY>
```

---

# What does API Key Identify?

> **API Key identifies the Application, NOT the User.**

Example

```text
Your Backend
      │
      ▼
OpenAI API

OpenAI identifies your Backend using the API Key.
```

---

# Common Use Cases

- OpenAI API
- Google Maps API
- Stripe API
- GitHub API
- AWS Services
- Weather APIs
- Twilio API

---

# Advantages

- Easy to implement.
- Fast authentication.
- Identifies applications.
- Supports rate limiting.
- Tracks API usage.

---

# Disadvantages

- Can be stolen if exposed.
- Does not authenticate users.
- Usually long-lived unless rotated.
- Cannot store user information.
- Must be protected carefully.

---

# API Key vs JWT

| API Key | JWT |
|----------|-----|
| Identifies an application | Identifies a user |
| Used between applications/services | Used after user login |
| Stores no user information | Stores user claims |
| Long-lived (typically) | Has expiration (`exp`) |
| Used for API authentication | Used for user authentication |

---

# API Key vs Session

| API Key | Session |
|----------|----------|
| Stateless | Stateful |
| Identifies application | Identifies logged-in user |
| No session storage required | Requires server-side session storage |
| Used for APIs | Used for web applications |

---

# Best Practices

- Store API Keys in **Environment Variables**.
- Never hardcode API Keys.
- Never expose API Keys in frontend code.
- Always use HTTPS.
- Rotate API Keys periodically.
- Restrict API Keys by permissions, IP, or domain whenever possible.

---

# Interview Questions

### What is an API Key?

> An API Key is a unique secret identifier used to authenticate and identify an application accessing an API.

---

### Why do we use API Keys?

- Authenticate applications.
- Control API access.
- Track usage.
- Apply rate limiting.

---

### Does an API Key authenticate a user?

> No. It authenticates an **application**, not a user.

---

### Where should API Keys be stored?

> In backend environment variables or a secure secrets manager.

---

### Can API Keys replace JWT?

> No. API Keys authenticate applications, whereas JWT authenticates users.

---

# Real-World Example

```text
User
   │
   ▼
Logs into Your Application (JWT)
   │
   ▼
Your Backend
   │
   ▼
Uses API Key
   │
   ▼
OpenAI API
```

- **JWT** → Authenticates the User.
- **API Key** → Authenticates the Backend Application.

---

# Memory Trick

Imagine a company office.

```text
Employee
     │
     ▼
Shows Company ID Card
     │
     ▼
Security Verifies
     │
     ▼
Entry Allowed
```

- **Company ID Card** → API Key
- **Security Guard** → API Server
- **Office Building** → Protected API

		 Customer
		     │
		     ▼
		 Pizza Shop
		     │
		     ▼
		Partner ID (API Key)
		     │
		     ▼
		Swiggy Server
		     │
		     ▼
		Valid Partner?
		     │
		 ┌───┴────┐
		 │        │
		Yes      No
		 │        │
		Deliver  Reject

# One-Line Notes

- **API Key:** A unique secret identifier used to authenticate and identify an application accessing an API.
- **Purpose:** Authenticates applications, controls access, tracks usage, and enables rate limiting.
- **Important:** API Keys identify **applications**, whereas JWTs identify **users**.
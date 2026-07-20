
> [!info] Definition
> **Request Context** is a temporary storage attached to a single HTTP request that stores information needed by different parts of the application while processing that request.
>
> It allows Middleware, Controllers, Services, and Repositories to share the same request-specific information without recalculating or fetching it again.

---

# Why Do We Need Request Context?

During a request, multiple layers may need the same information.

Examples:

- Authenticated User
- Request ID
- Logger
- Language
- Client IP
- Request Start Time

Instead of retrieving this information repeatedly, it is stored once in the Request Context and shared throughout the request lifecycle.

---

# How Request Context Works

```text
Client
   │
   ▼
HTTP Request
   │
   ▼
Authentication Middleware
(Verify JWT)
   │
   ▼
Create Request Context
(req.user, req.requestId, req.logger)
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Database
   │
   ▼
HTTP Response
```

---

# What Can Be Stored in Request Context?

Common information stored includes:

```javascript
req.user

req.requestId

req.language

req.logger

req.startTime

req.ip

req.permissions
```

Example

```javascript
req.user = {
    id: 101,
    name: "Goushik",
    role: "Employee"
}

req.requestId = "REQ-2026-001"

req.startTime = Date.now()
```

---

# Real-Life Example – Hospital

Imagine visiting a hospital.

## Step 1 – Reception

The receptionist creates a **Patient File**.

```text
Patient ID : 105
Name       : Goushik
Doctor     : Dr. Ravi
Blood Group: O+
```

---

## Step 2 – Doctor

The doctor reads the same file.

Adds:

```text
Diagnosis : Viral Fever
```

---

## Step 3 – Lab

The lab technician reads the same file.

Adds:

```text
Blood Test Completed
```

---

## Step 4 – Pharmacy

The pharmacist reads the same file and provides the medicine.

---

### Hospital Flow

```text
Patient
   │
   ▼
Reception
(Create Patient File)
   │
   ▼
Doctor
(Read & Update File)
   │
   ▼
Lab
(Read & Update File)
   │
   ▼
Pharmacy
(Read File)
```

### Mapping

```text
Patient File
        =
Request Context
```

Every department uses the same file.

Similarly,

Controller, Service, and Repository use the same Request Context.

---

# Backend Example

Suppose a user opens Amazon and clicks **My Orders**.

Browser sends:

```http
GET /orders
Authorization: Bearer JWT_TOKEN
```

---

## Authentication Middleware

Verifies the JWT.

Finds

```text
User ID : 101
Role    : Customer
```

Stores

```javascript
req.user = {
    id: 101,
    role: "Customer"
}
```

This becomes part of the Request Context.

---

## Controller

```javascript
function getOrders(req, res) {

    console.log(req.user.id);

}
```

Output

```text
101
```

---

## Service

```javascript
orderService.getOrders(req.user.id);
```

---

## Repository

```sql
SELECT *
FROM Orders
WHERE userId = 101;
```

The same Request Context is used throughout the request.

---

# Flow Diagram

```text
Client
   │
   ▼
HTTP Request
   │
   ▼
Authentication Middleware
   │
   ▼
Request Context Created
(req.user)
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Database
```

---

# Without Request Context

Every layer has to verify the JWT again.

```text
Controller
│
▼
Decode JWT

↓

Service

↓

Decode JWT Again

↓

Repository

↓

Decode JWT Again
```

This causes unnecessary work.

---

# With Request Context

```text
Authentication Middleware

↓

Verify JWT Once

↓

Store User in Request Context

↓

Controller

↓

Service

↓

Repository
```

Every layer simply reads the stored information.

---

# Lifetime of Request Context

> [!important]

Request Context exists **only for one HTTP request**.

```text
Request 1

↓

Context Created

↓

Response Sent

↓

Context Destroyed

--------------------------------

Request 2

↓

New Context Created

↓

Response Sent

↓

Context Destroyed
```

Each request gets its own independent Request Context.

---

# Advantages

> [!success]

- ✅ Shares data across application layers
- ✅ Avoids repeated computations
- ✅ Improves performance
- ✅ Cleaner code
- ✅ Better maintainability
- ✅ Keeps request-specific data organized

---

# Interview Definition

> Request Context is a temporary container attached to a single HTTP request that stores shared information such as authenticated user details, request ID, logger, and metadata, allowing different layers of the application to access the same data during request processing.

---

# One-Line Note

> **Request Context is a temporary storage created for each HTTP request to share request-specific information across Middleware, Controllers, Services, and Repositories.**

---

# Key Points

> [!tip]

- Created for every incoming HTTP request.
- Exists only during that request.
- Destroyed after the response is sent.
- Stores request-specific information.
- Accessible throughout the request lifecycle.
- Prevents repeated fetching or recalculating of the same data.
# Middleware (Express.js)

> [!info] Definition
> **Middleware** is a function that executes during the HTTP request lifecycle between the incoming client request and the final route handler (Controller).
>
> It acts as an intermediate layer where operations can be performed before the request reaches the business logic.

---

# Route Handler vs Middleware

## Route Handler

A Route Handler receives only **2 parameters**.

```javascript
(req, res)
```

- **req** → Request Object
- **res** → Response Object

A Route Handler is responsible for processing the request and sending the final response.

---

## Middleware

A Middleware receives **3 parameters**.

```javascript
(req, res, next)
```

- **req** → Request Object
- **res** → Response Object
- **next** → Function that transfers execution to the next middleware or route handler.

---

# Components of Middleware

## Request (req)

Contains all incoming request information.

Examples

- URL
- Request Body
- Query Parameters
- Path Parameters
- Headers
- Cookies

---

## Response (res)

Used to send the response back to the client.

Examples

```javascript
res.send()

res.json()

res.status(200).json()

res.redirect()
```

---

## Next (next)

> [!important]
> `next()` passes execution from the current middleware to the next middleware or the final route handler.

Example

```javascript
app.use((req, res, next) => {
    console.log("Middleware Executed");
    next();
});
```

---

# Execution Flow

```text
Client Request
      │
      ▼
Middleware 1
      │
   next()
      ▼
Middleware 2
      │
   next()
      ▼
Middleware 3
      │
   next()
      ▼
Route Handler (Controller)
      │
      ▼
HTTP Response
```

---

# How Middleware Works

```text
Client
   │
   ▼
Incoming HTTP Request
   │
   ▼
Middleware
   │
   ├── Perform Required Task
   │
   ├── Send Response
   │       │
   │       ▼
   │   Request Ends
   │
   └── next()
           │
           ▼
   Next Middleware
           │
           ▼
   Route Handler (Controller)
           │
           ▼
   HTTP Response
```

---

# Why Do We Use Middleware?

Instead of writing the same code in every API or Route Handler, we write it once as Middleware and reuse it wherever required.

This avoids duplicate code and keeps the application clean and maintainable.

---

# Common Uses of Middleware

- Authentication
- Authorization
- Logging
- Validation
- Transformation
- Error Handling
- Security Checks
- Rate Limiting
- CORS
- Request Body Parsing (`express.json()`)
- Compression

---

# Multiple Middleware Flow

```text
Client
   │
   ▼
Logger Middleware
   │
   ▼
Authentication Middleware
   │
   ▼
Authorization Middleware
   │
   ▼
Validation Middleware
   │
   ▼
Transformation Middleware
   │
   ▼
Controller (Route Handler)
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

# What Happens if next() is NOT Called?

### Case 1 — Middleware Sends Response

```javascript
function auth(req, res, next) {

    if (!req.headers.authorization) {
        return res.status(401).json({
            message: "Unauthorized"
        });
    }

    next();
}
```

Flow

```text
Client
   │
   ▼
Authentication Middleware
   │
   ▼
Unauthorized
   │
   ▼
401 Response
```

The request ends here.

The Controller is **never executed**.

---

### Case 2 — next() is Forgotten

```javascript
app.use((req, res, next) => {
    console.log("Request");
});
```

No response.

No `next()`.

The client keeps waiting until the request eventually times out.

---
# Categories (types) of middleware based on their purpose

- # **[[Security Middleware]]**
- # **[[Logging and Monitoring Middleware]]]**
- # **[[Global Error Handling Middleware]]]**
- # **[[Compression Middleware]]**
- # **[[Data Parsing Middleware]]**
  

---

# Global Middleware vs Route Middleware

## Global Middleware

Runs for every request.

```javascript
app.use(logger);
```

Flow

```text
Every Request
      │
      ▼
Logger Middleware
```

---

## Route Middleware

Runs only for a specific route.

```javascript
app.get("/users", authMiddleware, getUsers);
```

Flow

```text
GET /users
      │
      ▼
Authentication Middleware
      │
      ▼
Controller
```

---

# Advantages

> [!success]

- ✅ Code Reusability
- ✅ Cleaner Controllers
- ✅ Better Separation of Concerns
- ✅ Easy Maintenance
- ✅ Improved Readability
- ✅ Centralized Common Logic

---

# Simple Example

```javascript
function logger(req, res, next) {
    console.log("Request Received");
    next();
}

app.get("/users", logger, (req, res) => {
    res.send("Users List");
});
```

Execution

```text
GET /users
      │
      ▼
logger()
      │
      ▼
next()
      │
      ▼
Controller
      │
      ▼
Users List
```

---

# Middleware in the HTTP Request Lifecycle

```text
Client
   │
   ▼
HTTP Request
   │
   ▼
Middleware
(Logger, CORS, Rate Limiter)
   │
   ▼
Middleware
(Authentication)
   │
   ▼
Middleware
(Authorization)
   │
   ▼
Middleware
(Validation)
   │
   ▼
Middleware
(Transformation)
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

# Interview Definition

> Middleware is a reusable function that executes during the HTTP request lifecycle before the Controller. It can inspect, modify, validate, authenticate, authorize, or terminate a request before passing control to the next middleware or the Controller.

---

# Key Points

> [!tip]

- Middleware executes before the Controller.
- Multiple middlewares can execute sequentially.
- Every middleware receives `req`, `res`, and `next`.
- Calling `next()` passes control to the next middleware.
- Middleware can send a response directly without calling `next()`.
- If `next()` is not called and no response is sent, the request will remain pending.
- Middleware is mainly used to implement reusable logic shared across multiple routes.

---

# One-Line Note

> **Middleware = A reusable function that processes an HTTP request before it reaches the Controller.**
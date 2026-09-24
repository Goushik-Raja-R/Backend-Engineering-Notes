# Backend Engineering Notes

A structured collection of my backend engineering learning notes,
covering backend fundamentals, HTTP, authentication and authorization,
validation, application architecture, middleware, REST API design,
and databases.

These notes document concepts I have studied and explored while
building backend applications using Node.js, TypeScript, Express.js,
and PostgreSQL.

---

## 📚 Topics Covered

### 00 — Backend

Backend engineering fundamentals and the concepts required to
understand how backend applications work.

Topics covered:

- Backend fundamentals
- Client-server architecture
- Backend application concepts
- APIs
- Request and response concepts
- Runtime and framework fundamentals

---

### 01 — Understanding HTTP

Fundamentals of HTTP and how clients communicate with backend
applications.

Topics covered:

- HTTP fundamentals
- HTTP requests
- HTTP responses
- HTTP methods
- HTTP status codes
- HTTP headers
- Request body
- Query parameters
- Path parameters
- Cookies
- Content types
- Stateless communication

---

### 03 — Authentication and Authorizations

Understanding how backend applications authenticate users and
control access to protected resources.

Topics covered:

- Authentication
- Authorization
- Password authentication
- Password hashing
- JWT
- Access tokens
- Refresh tokens
- JWT verification
- Protected routes
- Role-Based Access Control (RBAC)
- Roles and permissions
- Authentication middleware
- Authorization middleware

---

### 04 — Validations and Transformations

Understanding how backend applications validate and transform
incoming request data.

Topics covered:

- Request validation
- Input validation
- Data validation
- Data transformation
- Request data handling
- Invalid input handling
- Validation boundaries

---

### 05 — Controllers - Services - Repositories - Req Context

Understanding how backend applications can separate responsibilities
into different layers.

Topics covered:

- Controllers
- Services
- Repositories
- Request context
- Separation of concerns
- Business logic
- Data access
- Layered architecture
- Request processing flow

Typical backend request flow:

```text
Client
  │
  ▼
Route
  │
  ▼
Middleware
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

### 06 — Middlewares

Understanding middleware and its role in processing requests before
they reach the final route handler.

Topics covered:

- Middleware fundamentals
- Middleware execution
- Authentication middleware
- Authorization middleware
- Validation middleware
- Rate limiting
- Error-handling middleware
- Middleware order
- Request processing pipeline

Example:

```text
Incoming Request
       │
       ▼
Authentication
       │
       ▼
Authorization
       │
       ▼
Validation
       │
       ▼
Controller
```

---

### 07 — Complete REST API Design

Understanding how to design structured and maintainable REST APIs.

Topics covered:

- REST fundamentals
- Resource-oriented API design
- HTTP methods
- HTTP status codes
- URL design
- Request structure
- Response structure
- CRUD operations
- Error responses
- Authentication
- Authorization
- API consistency

---

### 08 — Database

Database fundamentals and PostgreSQL concepts used in backend
application development.

Topics covered:

- Database fundamentals
- Relational databases
- PostgreSQL
- Tables
- Rows and columns
- Primary keys
- Foreign keys
- Constraints
- Relationships
- CRUD operations
- SQL queries
- SELECT
- WHERE
- AND / OR
- ORDER BY
- ASC / DESC
- Database persistence
- Database connections
- Connection pooling
- Database migrations

---

## 🛠️ Technology Focus

The concepts documented in this repository are primarily explored
using:

| Area | Technology |
|------|------------|
| Language | TypeScript |
| Runtime | Node.js |
| Framework | Express.js |
| API | REST APIs |
| Authentication | JWT |
| Authorization | RBAC |
| Database | PostgreSQL |
| Query Language | SQL |
| Version Control | Git & GitHub |

---

## 🔨 Practical Application

These notes are connected to practical backend development rather
than being only theoretical documentation.

The concepts documented here have been applied while building my
Authentication Service.

### 🔐 Authentication Service

A production-style authentication backend built using:

- TypeScript
- Node.js
- Express.js
- PostgreSQL
- JWT authentication
- Refresh tokens
- RBAC
- Rate limiting
- Docker
- Nginx
- AWS EC2

The project applies concepts covered throughout these notes,
particularly authentication, authorization, middleware, REST API
design, layered architecture, and PostgreSQL.

**Authentication Service:**

https://github.com/Goushik-Raja-R/Authentication-Service

---

## 🧠 Learning Approach

I use this repository to document concepts as I learn and apply them
in practical backend development.

The learning process follows:

```text
Learn
  │
  ▼
Understand
  │
  ▼
Implement
  │
  ▼
Debug
  │
  ▼
Document
  │
  ▼
Apply
```

The focus is on understanding how backend concepts work and how they
are used when building actual applications.

---

## 📈 Repository Structure

```text
Backend-Engineering-Notes/
│
├── 00 - Backend/
│
├── 01 - Understanding HTTP/
│
├── 03 - Authentication and Authorization/
│
├── 04 - Validations and Transformations/
│
├── 05 - Controllers - Services - Repositories - Req Context/
│
├── 06 - Middlewares/
│
├── 07 - Complete REST API Design/
│
└── 08 - Database/
```

Each section contains notes and learning material focused on a
specific area of backend engineering.

---

## 🚀 Current Focus

My current backend engineering focus is:

- TypeScript
- Node.js
- Express.js
- PostgreSQL
- REST API design
- Authentication & authorization
- Backend architecture
- Docker
- AWS deployment

---

## 🔗 Related

### GitHub

https://github.com/Goushik-Raja-R

### Authentication Service

https://github.com/Goushik-Raja-R/Authentication-Service

### LinkedIn

https://www.linkedin.com/in/goushikraja10/

---

## 📌 Note

This repository is continuously evolving as I learn and apply new
backend engineering concepts.

The notes represent my learning, implementation, debugging, and
practical exploration of backend development.


## Definition

**API Interface Design** is the process of designing how clients communicate with a backend through an API.

A good API should be:

- Consistent
- Predictable
- Easy to understand
- Easy to integrate
- Maintainable
- Follow common API/REST standards

---

# API Design Flow

```text
Business Requirements
        ↓
Identify Resources
        ↓
Identify Relationships
        ↓
Identify Operations
        ↓
Design Data Model
        ↓
Design API Contract
        ↓
Implement Backend
        ↓
Frontend / Client Consumes API
```

---

# 1. Business Requirements

Before designing an API, first understand:

> **What does the application need to do?**

### Example

> An employee can apply for leave.  
> A manager can approve or reject the leave request.

From this requirement, we identify:

### Entities / Resources

- Employee
- Leave Request
- Manager

### Actions / Operations

- Apply
- View
- Approve
- Reject

---

# 2. Identify Resources

## What is a Resource?

A **resource** is an important object or entity that the backend manages or exposes through an API.

Examples:

```text
Employee
Book
Product
Order
Leave Request
```

These can become API resources:

```http
/employees
/books
/products
/orders
/leave-requests
```

> [!warning]
> Not every noun automatically becomes an API resource or database table.
>
> We first need to understand the business domain.

### Example

A manager may simply be an employee with a different role:

```text
Employee
   └── role = MANAGER
```

So `Manager` does not necessarily need to become a separate resource.

---

# 3. Identify Relationships

After identifying resources, determine how they are related.

### Example

```text
Employee
    │
    │ creates
    ▼
Leave Request
    │
    │ approved / rejected by
    ▼
Manager
```

Possible relationships:

```text
Employee → creates → Leave Request

Manager → approves / rejects → Leave Request
```

Relationships are important for:

- Database design
- API design

---

# 4. Identify Operations

Operations represent **what users want to do** with the resources.

Example:

```text
Apply
View
Approve
Reject
```

For common CRUD operations, HTTP methods represent the operation:

```text
GET     → Retrieve
POST    → Create
PUT     → Replace
PATCH   → Partially Update
DELETE  → Delete
```

> [!important]
> In REST, we generally don't put every action into the URL.
>
> The **HTTP method + resource** usually expresses the operation.

---

# Resources vs Operations

## Resources = Nouns

Resources represent **things** that the application manages.

```text
Employee
Book
Product
Order
Leave Request
```

Example:

```http
/employees
/books
/products
/orders
/leave-requests
```

---

## Operations = Actions

Operations represent **what we do** with resources.

```text
Create
Retrieve
Update
Delete
Approve
Reject
```

Example:

```http
GET /employees
```

Means:

> Retrieve employees.

```http
POST /employees
```

Means:

> Create an employee.

---

# 5. Design API Endpoints

Once resources and operations are identified, design the API endpoints.

## Example — Leave Management

### Create Leave Request

```http
POST /leave-requests
```

Purpose:

```text
Employee applies for leave
```

---

### Get Leave Requests

```http
GET /leave-requests
```

Purpose:

```text
View leave requests
```

---

### Update Leave Request

```http
PATCH /leave-requests/{id}
```

Example:

```http
PATCH /leave-requests/501
```

Request:

```json
{
    "status": "APPROVED"
}
```

Purpose:

```text
Manager approves the leave request
```

---

# REST Resource Naming

## ❌ Avoid

```http
GET /getAllEmployees

POST /createEmployee

DELETE /deleteEmployee/101
```

## ✅ Prefer

```http
GET    /employees

POST   /employees

GET    /employees/101

DELETE /employees/101
```

### Why?

Because the HTTP method already tells us the action.

```text
GET    → Retrieve
POST   → Create
PUT    → Replace
PATCH  → Modify
DELETE → Delete
```

Therefore, the URL can focus on the **resource**.

---

# 6. Database Design

After understanding the resources and relationships, design the data model.

Database design focuses on:

```text
Tables
Columns
Primary Keys
Foreign Keys
Indexes
Relationships
Constraints
```

### Example

```text
Employee
    │
    │ 1
    │
    │
    │ Many
    ▼
Leave Request
```

Possible tables:

```text
employees
leave_requests
```

---

# API Design vs Database Design

## API Design

Concerned with:

```text
Resources
Endpoints
HTTP Methods
Request Body
Query Parameters
Path Parameters
Headers
Response Body
Status Codes
Authentication
Authorization
```

## Database Design

Concerned with:

```text
Tables
Columns
Primary Keys
Foreign Keys
Indexes
Relationships
Constraints
```

> [!important]
> **API = Interface exposed to clients**
>
> **Database = Internal storage used by the backend**

The client does not need to know how the database internally works.

---

# API Design and Database Design

API design and database design can influence each other.

They don't always have to happen in a strict sequence.

```text
             Business Requirements
                     ↓
                  Resources
                     ↓
                Relationships
                     ↓
              ┌──────┴──────┐
              ↓             ↓
         Data Model     API Contract
              │             │
              └──────┬──────┘
                     ↓
             Backend Implementation
```

Example:

```http
GET /employees/101/leave-requests
```

This indicates:

```text
Employee
    ↓
has
    ↓
Leave Requests
```

That relationship can influence the database design.

At the same time, the database model can influence the API design.

---

# Complete Backend Flow

Once the API is designed, the backend can implement it.

```text
Client
   ↓
HTTP Request
   ↓
Middleware
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
   ↓
Repository
   ↓
Service
   ↓
Controller
   ↓
HTTP Response
```

---

# Complete API Design Process

```text
Business Requirements
        ↓
Identify Resources
        ↓
Identify Relationships
        ↓
Identify Operations
        ↓
Design Data Model
        ↓
Design API Contract
        ↓
Implement Backend Logic
        ↓
Frontend / Client Consumes API
```

---

# Complete Example

## Business Requirement

> An employee can apply for leave. A manager can approve or reject the leave.

### Step 1 — Resources

```text
Employee
Leave Request
```

### Step 2 — Relationships

```text
Employee
    ↓
creates
    ↓
Leave Request
```

```text
Manager
    ↓
approves / rejects
    ↓
Leave Request
```

### Step 3 — Operations

```text
Apply
View
Approve
Reject
```

### Step 4 — API

```http
POST /leave-requests
GET /leave-requests
PATCH /leave-requests/{id}
```

### Step 5 — Backend Implementation

```text
Request
   ↓
Middleware
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

---

# Key Points

- API design starts from **business requirements**.
- Identify important **resources**.
- Resources are generally represented as **nouns**.
- Identify **relationships** between resources.
- Identify **operations / use cases**.
- REST APIs generally use **nouns in URLs**.
- HTTP methods represent common operations.
- Not every noun automatically becomes a resource.
- API design and database design can influence each other.
- API design defines the **contract between client and backend**.
- The frontend consumes the API according to the API contract.

---

# One-Line Revision

> **Business Requirements → Resources → Relationships → Operations → Data Model + API Contract → Backend Implementation**


> [!info] Definition
> **REST (Representational State Transfer)** is an architectural style for designing scalable and maintainable distributed systems, commonly used for Client-Server communication.

---

# REST Meaning

REST stands for:

```text
R → Representational
S → State
T → Transfer
```

---

# 1. Representation

> [!info] Definition
> **Representation** is the format in which a resource's state is represented and transferred between the Client and Server.

A resource can be:

- User
- Product
- Book
- Order

Example Resource:

```text
Book
```

Its representation can be JSON:

```json
{
    "id": 101,
    "name": "Clean Code",
    "price": 500
}
```

Common representations include:

- JSON
- XML
- HTML

> [!important]
> REST is commonly used for **Client-Server communication**, not specifically Server-to-Server communication.

---

# 2. State

> [!info] Definition
> **State** represents the current condition or information of a resource at a particular point in time.

Example:

```text
Book ID     → 101
Name        → Clean Code
Price       → $500
Stock       → 20
```

This represents the current state of the Book resource.

If the stock changes:

```text
Stock → 19
```

The state of the resource has changed.

---

## Important

> [!warning]
> REST's **State** does NOT mean that the server stores the user's previous requests.

That concept is related to **Stateful vs Stateless communication**.

---

# 3. Transfer

> [!info] Definition
> **Transfer** is the process of transferring a representation of a resource's state between the Client and Server.

Example:

```text
Client
   │
   │ GET /books/101
   ▼
Server
   │
   │ JSON Representation
   ▼
Client
```

Response:

```json
{
    "id": 101,
    "name": "Clean Code",
    "price": 500
}
```

---

# REST Example

Request:

```http
GET /books/101
```

### Resource

```text
Book #101
```

### Current State

```json
{
    "id": 101,
    "name": "Clean Code",
    "price": 500
}
```

### Representation

```text
JSON
```

### Transfer

```text
Server ──────────────► Client
         JSON Response
```

---

# REST URL Structure

Example:

```text
https://api.example.com/v1/books
```

Breakdown:

```text
https://api.example.com/v1/books
│      │              │  │
│      │              │  └── Resource
│      │              └───── API Version
│      └──────────────────── Host / Domain
└─────────────────────────── Scheme
```

More specifically:

```text
https://
   ↓
Scheme

api
   ↓
Subdomain

example.com
   ↓
Domain

/v1
   ↓
API Version

/books
   ↓
Resource Collection
```

---

# URL Structure

A URL can contain:

```text
scheme://host/path?query#fragment
```

Example:

```text
https://sriniously.xyz/blog/zist?q=something#headers
```

```text
https://        → Scheme
sriniously.xyz  → Host / Domain
/blog/zist      → Path
?q=something    → Query Parameter
#headers        → Fragment
```

---

# Resource Naming

REST APIs generally use **plural nouns** for resource collections.

Example:

```text
/books
/users
/products
/orders
```

Instead of:

```text
/book
/user
/product
/order
```

---

# Collection vs Individual Resource

## Collection

```http
GET /books
```

Means:

> Get the collection of books.

Conceptually:

```text
/books
   │
   ├── Book 101
   ├── Book 102
   └── Book 103
```

---

## Specific Resource

```http
GET /books/101
```

Means:

> Get the specific book whose ID is 101.

```text
/books
   │
   ├── /101
   ├── /102
   └── /103
```

---

# Path Parameter vs Query Parameter

> [!important]
> `/books/101` and `/books?id=101` are different concepts.

## Path Parameter

```http
GET /books/101
```

```text
/books/101
       ↑
       Path Parameter
```

Used when identifying a **specific resource**.

---

## Query Parameter

```http
GET /books?id=101
```

```text
/books?id=101
       ↑
       Query Parameter
```

Usually used for:

- Filtering
- Searching
- Sorting
- Pagination

Example:

```http
GET /books?author=Robert
```

Means:

> Find books where the author is Robert.

---

# Hierarchical Relationship

The `/` in a URL can represent a hierarchical relationship between resources.

Example:

```text
/users/101/orders/500
```

Can be understood as:

```text
Users
  │
  └── User 101
          │
          └── Orders
                 │
                 └── Order 500
```

Another example:

```text
/books/101/reviews
```

Means:

> Reviews belonging to Book 101.

---

# REST Mental Model

```text
                    REST
                      │
          ┌───────────┼───────────┐
          │           │           │
 Representation      State      Transfer
          │           │           │
        JSON       Current      Moving the
                   condition    representation
                   of resource  between Client
                                and Server
```

---

# Complete Example

```text
Client
   │
   │ GET /books/101
   ▼
Server
   │
   │ Resource → Book 101
   │
   │ State:
   │ {
   │   id: 101,
   │   name: "Clean Code",
   │   price: 500
   │ }
   │
   │ Representation → JSON
   │
   ▼
Client
```

---

# REST vs HTTP

| REST | HTTP |
|---|---|
| Architectural Style | Communication Protocol |
| Defines principles for designing distributed systems | Defines how Client and Server communicate |
| Focuses on scalable and maintainable architecture | Handles requests and responses |
| Commonly implemented using HTTP | Commonly used to implement REST APIs |

> [!warning]
> **REST ≠ HTTP**
>
> REST is an architectural style, while HTTP is a communication protocol.

---

# Key Points

> [!tip]

- REST = **Representational State Transfer**
- REST is an **architectural style**, not a protocol.
- Representation = Format used to represent a resource's state.
- State = Current condition/information of a resource.
- Transfer = Moving the representation between Client and Server.
- JSON is the most commonly used representation in REST APIs.
- `/books` represents a collection of books.
- `/books/101` identifies a specific book.
- `/books/101` → Path Parameter.
- `/books?id=101` → Query Parameter.
- `/` can express hierarchical relationships.
- REST is commonly used for Client-Server communication.

---

# One-Line Revision

> **REST is an architectural style where the current state of resources is represented in a format such as JSON and transferred between Client and Server.**
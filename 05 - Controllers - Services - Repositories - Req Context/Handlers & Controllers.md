
## Definition

> A **Controller (Handler)** is responsible for receiving the HTTP request, coordinating with the service layer, and returning the HTTP response.

---

# Responsibilities

- Receive HTTP requests.
- Read Request Body, Query Parameters, Path Parameters and Headers.
- Call the appropriate Service.
- Return the HTTP response.
- Handle HTTP status codes.

---

# HTTP Methods

### GET

Usually receives data through:

- Query Parameters
- Path Parameters

Example

```http
GET /books?author=John
```

---

### POST

Usually receives data through:

```http
POST /books
```

Request Body

```json
{
    "name":"Atomic Habits"
}
```

---

### PUT / PATCH

Receives updated data through Request Body.

---

### DELETE

Usually identifies the resource using:

- Path Parameter
- Query Parameter

Example

```http
DELETE /books/10
```

(Some APIs also accept Request Body.)

---

# Responsibilities of Controller

Request
↓

Deserialization

↓

Binding

↓

Validation

↓

Transformation

↓

Service

↓

HTTP Response

---

# One-Line Note

> **Controller = Handles HTTP requests and responses, then delegates business logic to the Service layer.**
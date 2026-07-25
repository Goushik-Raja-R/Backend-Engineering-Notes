

> [!info] Definition
> **Idempotency** means that making the same request multiple times produces the **same final effect on the server state** as making the request once.

### Important

> [!warning]
> Idempotency does **NOT** mean that every repeated request must return the same response.

The important thing is the **final state of the server**.

---

# Simple Example

Consider:

```http
DELETE /users/101
```

### First Request

```text
User 101 exists
      ↓
DELETE
      ↓
User 101 deleted
```

Response:

```text
204 No Content
```

### Second Request

```text
User 101 does not exist
      ↓
DELETE
      ↓
Nothing changes
```

Response:

```text
404 Not Found
```

The responses are different:

```text
1st → 204
2nd → 404
```

But the final state is the same:

```text
User 101 → Does not exist
```

Therefore:

> **DELETE is idempotent.**

---

# Idempotent vs Non-Idempotent

## Idempotent

If we send the same request multiple times:

```text
Request × 1
Request × 100
       ↓
Same final server state
```

---

## Non-Idempotent

If we send the same request multiple times:

```text
Request × 1
Request × 100
       ↓
Different final server state
```

---

# HTTP Methods and Idempotency

| HTTP Method | Idempotent? | Typical Purpose |
|---|---|---|
| GET | ✅ Yes | Retrieve resource |
| POST | ❌ No | Create / Process |
| PUT | ✅ Yes | Replace resource |
| PATCH | ⚠️ Depends | Partially modify resource |
| DELETE | ✅ Yes | Delete resource |

---

# GET → Idempotent

```http
GET /users/101
```

The request only retrieves data.

Calling it multiple times:

```text
GET /users/101
GET /users/101
GET /users/101
```

does not normally change the user's data.

```text
Final State → Same
```

Therefore:

> **GET is idempotent.**

---

# PUT → Idempotent

PUT is generally used to **replace the complete representation of a resource**.

```http
PUT /users/101
```

```json
{
    "name": "Goushik",
    "age": 22,
    "city": "Hyderabad"
}
```

If the same request is sent 100 times:

```text
Request 1 → User replaced with given data
Request 2 → Same replacement
Request 3 → Same replacement
...
Request 100 → Same replacement
```

Final state remains the same.

Therefore:

> **PUT is idempotent.**

---

# PATCH → Depends

PATCH is used to **partially modify a resource**.

PATCH can be idempotent or non-idempotent depending on the operation.

---

## Idempotent PATCH

```http
PATCH /users/101
```

```json
{
    "name": "Goushik"
}
```

Calling it repeatedly:

```text
name = Goushik
name = Goushik
name = Goushik
```

Final state remains the same.

Therefore, this PATCH operation is **idempotent**.

---

## Non-Idempotent PATCH

Imagine an API that increments a user's age:

```http
PATCH /users/101
```

```json
{
    "operation": "incrementAge"
}
```

First request:

```text
Age: 22 → 23
```

Second request:

```text
Age: 23 → 24
```

Third request:

```text
Age: 24 → 25
```

The final state keeps changing.

Therefore, this PATCH operation is **non-idempotent**.

> [!important]
> **PATCH is not inherently idempotent.**
> Its idempotency depends on how the API operation is designed.

---

# DELETE → Idempotent

```http
DELETE /users/101
```

First request:

```text
User exists
    ↓
Delete User
    ↓
User does not exist
```

Second request:

```text
User does not exist
    ↓
Nothing changes
```

Third request:

```text
User does not exist
    ↓
Nothing changes
```

Even if the second and third requests return:

```text
404 Not Found
```

the final state remains:

```text
User 101 → Does not exist
```

Therefore:

> **DELETE is idempotent.**

---

# POST → Non-Idempotent

POST is commonly used to create a new resource.

```http
POST /books
```

```json
{
    "name": "Clean Code"
}
```

First request:

```text
Book 101 created
```

Second identical request:

```text
Book 102 created
```

Third:

```text
Book 103 created
```

Every request creates a new resource.

```text
1 request  → 1 book
2 requests → 2 books
3 requests → 3 books
```

The final state keeps changing.

Therefore:

> **POST is non-idempotent.**

---

# POST for Actions

POST can also be used for operations that don't naturally map to another HTTP method.

Example:

```http
POST /emails/send
```

```json
{
    "to": "user@example.com",
    "subject": "Hello"
}
```

First request:

```text
Email sent
```

Second request:

```text
Another email sent
```

The side effect happens again.

Therefore:

> **POST is generally non-idempotent.**

---

# The Key Concept

> [!important]
> **Idempotency is about the final server state, NOT about getting the same response.**

Ask yourself:

> **"If I send the exact same request 100 times, is the final server state the same as if I had sent it only once?"**

### YES

```text
→ Idempotent
```

### NO

```text
→ Non-Idempotent
```

---

# Idempotency Mental Model

```text
              Same Request
                   │
          ┌────────┼────────┐
          │        │        │
        Call 1   Call 2   Call 100
          │        │        │
          └────────┼────────┘
                   ▼
             Final State
                   │
            ┌──────┴──────┐
            │             │
        Same State    Different State
            │             │
            ▼             ▼
       Idempotent    Non-Idempotent
```

---

# Real-Life Example

Imagine a light switch.

### Idempotent operation

```text
"Set the light to OFF"
```

Doing it once:

```text
OFF
```

Doing it 100 times:

```text
OFF
```

Final state is the same.

---

### Non-Idempotent operation

Imagine a button:

```text
"Toggle the light"
```

Every time you press it:

```text
OFF → ON
ON → OFF
OFF → ON
```

Repeated requests keep changing the state.

Therefore:

```text
Set OFF    → Idempotent
Toggle     → Non-Idempotent
```

---

# Key Points

> [!tip]

- Idempotency is about **server state**, not response equality.
- Repeating an idempotent request produces the same **final state**.
- GET is idempotent.
- PUT is idempotent.
- DELETE is idempotent.
- POST is generally non-idempotent.
- PATCH can be idempotent or non-idempotent depending on the operation.
- An idempotent request can still return an **error** on repeated calls.
- DELETE returning `404` on the second call does **not** make DELETE non-idempotent.

---

# One-Line Revision

> **Idempotency means sending the same request multiple times has the same effect on the final server state as sending it once.**
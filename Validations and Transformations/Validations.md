
## Definition

Validation is the process of verifying that the incoming request data is correct, complete, and follows the expected rules **before it reaches the controller**.

> **Validation = Checking whether the client's input is valid before processing the request.**

---

# Types of Validation

## 1. [[Syntactic Validation]]

---

## 2. [[Semantic Validation]]

---

## 3. [[Type Validation]]

---

# Request Flow

Validation is performed **before the request reaches the controller**.

```text
                Client
                   │
                   ▼
            Incoming Request
                   │
                   ▼
             Validation Layer
     (Syntactic / Semantic / Type)
                   │
          ┌────────┴────────┐
          │                 │
      Validation        Validation
        Failed            Passed
          │                 │
          ▼                 ▼
   Return Error         Controller
     (400 Bad Request)      │
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
                     Repository
                            │
                            ▼
                        Service
                            │
                            ▼
                       Controller
                            │
                            ▼
                  Response to Client
```

---

# Backend Request Lifecycle

```text
Client
   │
   ▼
Request
   │
   ▼
Validation
(Syntactic / Semantic / Type)
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
Repository
   │
   ▼
Service
   │
   ▼
Controller
   │
   ▼
Response
   │
   ▼
Client
```

---

# [[Frontend Validations vs Backend Validations]]

---


# Interview Definition

> Validation is the process of verifying that incoming request data satisfies syntax rules, business rules, and expected data types before it reaches the controller or business logic.

---

# One-Line Notes

- **Validation = Verify incoming data before processing it.**
- **Syntactic Validation = Checks the format of the data.**
- **Semantic Validation = Checks business rules.**
- **Type Validation = Checks whether the data type is correct.**
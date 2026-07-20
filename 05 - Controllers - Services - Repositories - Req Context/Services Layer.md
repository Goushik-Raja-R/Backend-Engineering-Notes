
## Definition

> The **Service Layer** contains the application's business logic.

---

# Responsibilities

- Apply business rules.
- Process application logic.
- Coordinate multiple repositories.
- Return processed data.

---

# Service Does NOT

- Read HTTP Requests.
- Return HTTP Responses.
- Handle Status Codes.
- Access req or res objects.

---

# Example

Controller

↓

Service

↓

UserRepository

↓

EmailRepository

↓

NotificationRepository

↓

Return Result

---

# Example

Create User

↓

Check Email Exists

↓

Hash Password

↓

Save User

↓

Send Welcome Email

↓

Return User

---

# One-Line Note

> **Service = Executes business logic independent of HTTP.**
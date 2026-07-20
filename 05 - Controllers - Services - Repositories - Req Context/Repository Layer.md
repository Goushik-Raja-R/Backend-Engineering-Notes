
## Definition

> The **Repository Layer** is responsible for communicating with the database.

---

# Responsibilities

- Create Data
- Read Data
- Update Data
- Delete Data

(CRUD)

---

# Repository Does NOT

- Perform Business Logic.
- Handle HTTP Requests.
- Validate Data.

---

# Example

UserRepository

↓

Database

↓

Return User Data

---

# CRUD Operations

Create

↓

Read

↓

Update

↓

Delete

---

# One-Line Note

> **Repository = Handles database operations only.**
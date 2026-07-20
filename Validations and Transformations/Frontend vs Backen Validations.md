
## Frontend Validation

### Definition

> Validation performed in the client application before sending the request.

### Purpose

- Improve User Experience.
- Instant feedback.
- Reduce unnecessary API calls.

### Examples

- Required fields
- Email format
- Password length
- Mobile number length

---

## Backend Validation

### Definition

> Validation performed on the server before processing the request.

### Purpose

- Protect the application.
- Prevent malicious requests.
- Ensure data integrity.
- Prevent invalid data from entering the database.

---

# Example

Frontend validates:

```text
Age >= 18
```

Attacker bypasses the frontend using Postman:

```json
{
  "age": 10
}
```

Backend validation rejects the request.

---

# Comparison

| Frontend Validation | Backend Validation |
|---------------------|-------------------|
| Runs in Browser | Runs on Server |
| Improves User Experience | Protects the Application |
| Can be bypassed | Cannot be bypassed (if implemented correctly) |
| Optional | Mandatory |
| Fast feedback | Final validation before processing |

---

# Request Flow

User
↓
Frontend Validation
↓
API Request
↓
Backend Validation
↓
Controller
↓
Service
↓
Database

---

# Interview Definition

**Frontend Validation**

> Improves user experience by validating data before sending the request.

**Backend Validation**

> Protects the application by validating all incoming requests before processing.

---

# One-Line Note

> **Frontend Validation = Better user experience.**

> **Backend Validation = Application security and data integrity.**
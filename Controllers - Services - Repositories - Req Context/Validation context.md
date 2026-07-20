
## Definition

> **Validation** verifies whether the incoming request satisfies the application's rules.

---

# Examples

- Required Fields
- Email Format
- Password Length
- Mobile Number Length
- Age Validation

---

# Example

Input

```json
{
   "email":"abc"
}
```

↓

Response

```http
400 Bad Request
```

---

# Purpose

- Prevent invalid data.
- Protect the application.
- Ensure data integrity.

---

# One-Line Note

> **Validation = Checks whether incoming data is valid before processing.**
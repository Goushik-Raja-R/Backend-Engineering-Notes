
## Definition

> **Complex Validation** verifies business rules by checking relationships between multiple fields or external data.

---

# Why do we need Complex Validation?

Some validations cannot be performed by checking a single field.

They require:

- Multiple fields
- Business rules
- Database checks

---

# Examples

### Password Confirmation

```json
{
  "password": "Captain@123",
  "confirmPassword": "Captain@123"
}
```

Rule

```text
password === confirmPassword
```

---

### Hotel Booking

```json
{
  "checkIn": "20-07-2026",
  "checkOut": "18-07-2026"
}
```

Rule

```text
Check-out date must be after Check-in date.
```

---

### Product Discount

```json
{
  "price": 1000,
  "discount": 1200
}
```

Rule

```text
Discount cannot exceed the product price.
```

---

### Employee Registration

```json
{
  "role": "Employee",
  "managerId": 101
}
```

Rule

```text
Employees must have a valid managerId.
```

---

# Characteristics

- Checks multiple fields.
- Applies business rules.
- May query the database.
- Cannot be solved with simple syntax validation.

---

# Interview Definition

> Complex validation verifies business rules involving multiple fields or database relationships.

---

# One-Line Note

> **Complex Validation = Validate business rules involving multiple fields or database data.**
## Definition

> **Binding** maps the deserialized request data into application objects (DTOs/Models).

---

# Example

Incoming JSON

```json
{
   "name":"Goushik",
   "age":22
}
```

↓

Bound to

```javascript
UserDTO {
   name,
   age
}
```

---

# If Binding Fails

Malformed JSON

```json
{
 name:
```

↓

Response

```http
400 Bad Request
```

---

# One-Line Note

> **Binding = Mapping request data into application objects.**
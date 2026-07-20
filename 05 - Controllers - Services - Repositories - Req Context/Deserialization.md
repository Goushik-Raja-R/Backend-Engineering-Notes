
## Definition

> **Deserialization** is the process of converting incoming JSON data into native JavaScript objects.

---

# Node.js

In Express.js

```javascript
app.use(express.json());
```

This middleware converts:

Input

```json
{
    "name":"Goushik"
}
```

↓

Output

```javascript
req.body = {
   name:"Goushik"
}
```

---

# Why do we need Deserialization?

- Convert JSON into JavaScript Objects.
- Allow the application to access request data.

---

# One-Line Note

> **Deserialization = JSON → JavaScript Object**
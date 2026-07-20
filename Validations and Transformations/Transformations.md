
## Definition

> **Transformation** is the process of converting incoming request data into the format expected by the application before processing.

---

# Why do we need Transformation?

- Convert data into the correct type.
- Clean incoming data.
- Normalize data before business logic.

---

# Common Transformations

### String → Number

Input

```json
{
  "age": "22"
}
```

Output

```javascript
age = 22
```

---

### String → Boolean

Input

```json
{
  "isActive": "true"
}
```

Output

```javascript
isActive = true
```

---

### String → Date

Input

```json
{
  "dateOfBirth": "2002-06-12"
}
```

Output

```javascript
Date("2002-06-12")
```

---

### Trim Spaces

Input

```text
"   Goushik Raja   "
```

Output

```text
"Goushik Raja"
```

---

### Convert to Lowercase

Input

```text
GOUSHIK@GMAIL.COM
```

Output

```text
goushik@gmail.com
```

---

# Request Flow

Client
↓
Validation
↓
Transformation
↓
Controller

---

# Interview Definition

> Transformation converts valid incoming data into the format expected by the application before processing.

---

# One-Line Note

> **Transformation = Convert data into the required format before processing.**

---

# Important Note

- # **[[Complex Validations]]**
  
- # **[[Data Transformations]]**
  
- # **[[Frontend vs Backen Validations]]**
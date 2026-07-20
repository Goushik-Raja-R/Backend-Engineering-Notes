
## Definition

> **Transformation** converts valid incoming data into the format expected by the application.

---

# Examples

### Trim Spaces

```text
"  Goushik Raja  "

↓

"Goushik Raja"
```

---

### String → Number

```json
{
   "age":"22"
}
```

↓

```javascript
age = 22
```

---

### String → Boolean

```json
{
   "isActive":"true"
}
```

↓

```javascript
isActive = true
```

---

### Convert Email to Lowercase

```text
GOUSHIK@GMAIL.COM

↓

goushik@gmail.com
```

---

# Purpose

- Standardize data.
- Convert data types.
- Clean incoming data.

---

# One-Line Note

> **Transformation = Converts data into the application's expected format.**
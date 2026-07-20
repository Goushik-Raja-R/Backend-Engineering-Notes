

> [!info] Definition
> Data Parsing Middleware converts incoming HTTP request data into a format that the application can understand.

---

# Purpose

- Parse JSON
- Parse Form Data
- Parse URL-Encoded Data
- Make request data available in `req.body`

---

# Example

Client Sends

```json
{
    "name":"Goushik"
}
```

↓

Using

```javascript
app.use(express.json());
```

↓

Controller Receives

```javascript
req.body = {
    name: "Goushik"
}
```

---

# How It Works

Client
│
▼
Raw HTTP Request
│
▼
Data Parsing Middleware
│
▼
JavaScript Object
│
▼
Controller

---

# Real-Life Example

Imagine receiving a letter written in Japanese.

A translator converts it into English before you read it.

The translator is like Data Parsing Middleware—it converts data into a format you can understand.

---

# Common Parsers

- express.json()
- express.urlencoded()

---

# Advantages

- Makes request data easy to access
- Converts raw data into usable objects
- Simplifies request processing

---

# One-Line Note

> Data Parsing Middleware converts raw request data into JavaScript objects that the application can use.


> [!info] Definition
> Global Error Handling Middleware catches unhandled errors and returns a consistent error response to the client.

---

# Purpose

- Catch unexpected errors
- Prevent application crashes
- Return standardized error responses
- Centralize error handling

---

# Example

```javascript
app.use((err, req, res, next) => {
    res.status(500).json({
        message: err.message
    });
});
```

---

# How It Works

Controller
│
▼
Service
│
▼
Error Occurs
│
▼
Global Error Handler
│
▼
HTTP Error Response

---

# Real-Life Example

Imagine a shopping mall.

Whenever a customer has a complaint, they go to the **Customer Support Desk** instead of each individual shop.

The support desk handles every complaint consistently.

Similarly, Global Error Handling Middleware handles errors from anywhere in the application.

---

# Advantages

- Centralized error handling
- Cleaner code
- Consistent error responses
- Better user experience

---

# One-Line Note

> Global Error Handling Middleware catches application errors and returns a consistent response.
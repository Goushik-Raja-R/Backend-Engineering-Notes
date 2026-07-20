
> [!info] Definition
> Compression Middleware reduces the size of the HTTP response before sending it to the client.

---

# Purpose

- Reduce response size
- Improve application performance
- Save network bandwidth
- Speed up page loading

---

# Example

Without Compression

500 KB

↓

With Compression

80 KB

---

# How It Works

Controller
│
▼
Response
│
▼
Compression Middleware
│
▼
Compressed Response
│
▼
Client

---

# Real-Life Example

Imagine packing clothes into a vacuum storage bag.

The clothes remain the same, but they occupy much less space.

Compression Middleware does the same for HTTP responses.

---

# Popular Package

- compression

---

# Advantages

- Faster responses
- Reduced bandwidth usage
- Improved user experience

---

# One-Line Note

> Compression Middleware reduces the size of the response before sending it to the client.
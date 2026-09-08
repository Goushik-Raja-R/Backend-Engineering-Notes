
---

# 1. Client-Server Request Flow

The **client never accesses the database directly**.

> [!important]  
> ==The server acts as an intermediary between the client and the database.==

The client sends a request to the server, and the server communicates with the database when required.

### Complete Flow

```text
Browser
   ↓
DNS
   ↓
Find IP
   ↓
HTTP Request
   ↓
Nginx
   ↓
Node.js
   ↓
Database
   ↓
Node.js
   ↓
Nginx
   ↓
Browser
```

### Explanation

1. **Browser** initiates the request.
    
2. **DNS** helps find the IP address of the server.
    
3. Browser sends an **HTTP request**.
    
4. **Nginx** receives the request.
    
5. Nginx forwards the request to **Node.js**.
    
6. Node.js communicates with the **database**.
    
7. Database sends the result back to Node.js.
    
8. Node.js sends the response to Nginx.
    
9. Nginx sends the response back to the browser.
    

> [!important]  
> **Client → Server → Database**
> 
> The client does **not** directly communicate with the database.

---

# 2. Persistent Connection

A **persistent connection** means that the TCP connection stays open after the first request.

This allows multiple HTTP requests to use the **same TCP connection**.

> [!important]  
> ==One TCP connection can be reused for multiple HTTP requests and responses.==

### Without Persistent Connection

```text
Connect
   ↓
Request 1
   ↓
Response 1
   ↓
Disconnect
```

For another request, a new connection needs to be established.

### With Persistent Connection

```text
Connect
   ↓
Request 1
   ↓
Response 1
   ↓
Request 2
   ↓
Response 2
   ↓
Request 3
   ↓
Response 3
   ↓
Disconnect
```

### Why Persistent Connections?

Instead of repeatedly creating and closing TCP connections, the same connection can be reused.

> [!tip]  
> **Interview Point:**
> 
> **Persistent connection = Reuse the same TCP connection for multiple HTTP requests.**

---

# 3. HTTP Multiplexing

## What is Multiplexing?

**Multiplexing** means multiple HTTP requests and responses can travel simultaneously over the **same TCP connection**.

> [!important]  
> ==Multiple HTTP requests and responses can share the same TCP connection.==

### Example

```text
                 ┌── Request 1 ──┐
Browser ─────────┼── Request 2 ──┼────→ Server
                 └── Request 3 ──┘
                    Same TCP
                   Connection
```

The server can process multiple requests and return their responses independently.

### Example Flow

```text
Browser
   ↓
Request 1
Request 2
Request 3
   ↓
Server processes them
   ↓
Response 1
Response 2
Response 3
```

> [!tip]  
> **Multiplexing**
> 
> Multiple requests/responses → **Same TCP connection**

---

# 4. HTTP Headers

An **HTTP header** is metadata/information about an HTTP request or response.

Headers provide additional information about the HTTP message.

### HTTP Message Structure

```text
HTTP Message
│
├── Headers
│
└── Body
```

Example analogy:

```text
To: Amazon Warehouse
From: Goushik
Priority: Express
Weight: 2kg
-------------------
Actual Item: Laptop
```

Here:

- **Laptop** → Body
    
- **To, From, Priority, Weight** → Headers
    

HTTP works in a similar way.

> [!important]  
> ==Headers contain metadata about the HTTP request or response.==
> 
> The **body contains the actual data/payload**.

---

# 5. Types of HTTP Headers

The notes categorize HTTP headers into four major types:

```text
HTTP Headers
│
├── Request Headers
├── General Headers
├── Representation Headers
└── Security Headers
```

---

## 5.1 Request Headers

Request headers are sent by the **client**.

They describe information about the request or client.

### Examples

- `Authorization`
    
- `Host`
    
- `Accept`
    
- `User-Agent`
    

> [!important]  
> **Request Headers → Client → Server**

---

## 5.2 General Headers

General headers can be sent by the **client or server**.

They apply to the HTTP message itself.

### Examples

- `Connection`
    
- `Cache-Control`
    

> [!note]  
> General headers provide information/control related to the HTTP message and connection.

---

## 5.3 Representation Headers

Representation headers are generally associated with the representation/data being transferred.

They describe the content/body.

### Examples

- `Content-Type`
    
- `Content-Length`
    
- `Content-Encoding`
    

> [!important]  
> ==Representation headers describe the representation/content being transferred.==

---

## 5.4 Security Headers

Security headers are used to improve browser and application security.

### Examples

- `Strict-Transport-Security`
    
- `Content-Security-Policy`
    
- `X-Frame-Options`
    

> [!important]  
> ==Security headers help protect applications against different types of browser-based attacks.==

---

# 6. HTTP Methods

HTTP methods define the **action** that the client wants to perform.

|Method|Purpose|
|---|---|
|`GET`|Retrieve data|
|`POST`|Submit data for processing / create a resource|
|`PUT`|Create or completely replace a resource|
|`PATCH`|Partially update a resource|
|`DELETE`|Remove a resource|
|`HEAD`|Retrieve response headers only|
|`OPTIONS`|Retrieve supported methods/communication options|
|`TRACE`|Echo the request for diagnostic purposes|
|`CONNECT`|Establish a tunnel, typically through a proxy|

---

## GET

Retrieves data without modifying the resource.

```http
GET /users
```

> [!important]  
> ==GET is generally used for retrieving data.==

---

## POST

Submits data for processing or resource creation.

```http
POST /users
```

Example:

```json
{
  "name": "Goushik",
  "email": "goushik@example.com"
}
```

> [!important]  
> **POST** is commonly used when sending data to the server for processing or creating a resource.

---

## PUT

Creates or completely replaces a resource.

```http
PUT /users/101
```

> [!note]  
> **PUT** generally represents a complete replacement/update of a resource.

---

## PATCH

Partially updates a resource.

```http
PATCH /users/101
```

Example:

```json
{
  "name": "Goushik Raja"
}
```

Only the specified field needs to be updated.

---

## DELETE

Removes a resource from the server.

```http
DELETE /users/101
```

---

## HEAD

Retrieves the response headers without the response body.

```http
HEAD /users
```

> [!important]  
> ==HEAD is similar to GET, but the server does not return the response body.==

---

## OPTIONS

Returns information about supported methods and communication options.

```http
OPTIONS /users
```

> [!tip]  
> **OPTIONS is especially important when learning CORS**, because browsers may use an OPTIONS request as a **preflight request**.

---

## TRACE

Used for diagnostic purposes by echoing the received request.

```http
TRACE /users
```

> [!warning]  
> TRACE can have security implications and is commonly disabled on production servers.

---

## CONNECT

Establishes a tunnel through a proxy, commonly for HTTPS traffic.

```http
CONNECT example.com:443
```

---

# 7. Idempotent HTTP Methods

## What does Idempotent Mean?

An HTTP method is **idempotent** when making the **same request multiple times produces the same intended final result on the server**.

> [!important]  
> ==Same request repeated multiple times → Same final server state.==

### Idempotent Methods

From your notes:

```text
GET
PUT
DELETE
HEAD
OPTIONS
```

### Example

```text
PUT /users/101
```

Sending the same request multiple times should result in the resource having the same final state.

```text
Request
   ↓
Request
   ↓
Request
   ↓
Same final state
```

> [!tip]  
> **Interview Shortcut**
> 
> Idempotent:
> 
> `GET` → ✅  
> `PUT` → ✅  
> `DELETE` → ✅  
> `HEAD` → ✅  
> `OPTIONS` → ✅

---

# 8. Non-Idempotent HTTP Methods

A **non-idempotent method** can produce a different result when the same request is repeated.

From your notes:

```text
POST
PATCH
```

### Example

```http
POST /orders
```

If the same request is sent multiple times:

```text
POST
 ↓
Order 1 created

POST
 ↓
Order 2 created

POST
 ↓
Order 3 created
```

The result can be different each time.

> [!important]  
> ==Non-idempotent → Repeating the same request can change the server state again.==

### Quick Comparison

|Type|Methods|
|---|---|
|**Idempotent**|GET, PUT, DELETE, HEAD, OPTIONS|
|**Non-idempotent**|POST, PATCH|

---

# 9. CORS

## What is CORS?

**CORS** stands for:

> **Cross-Origin Resource Sharing**

CORS is a browser security mechanism that controls whether a web page from one **origin** can access resources from another origin.

---

# 10. What is an Origin?

An origin is made up of:

```text
Protocol + Domain + Port
```

> [!important]  
> ==Origin = Protocol + Domain + Port==

For example:

```text
https://shop.com
```

and

```text
http://shop.com
```

are different origins because the **protocol is different**.

---

## Same Origin Example

```text
Frontend:
https://shop.com

Backend:
https://shop.com
```

These have the same:

```text
Protocol → HTTPS
Domain   → shop.com
Port     → same/default
```

Therefore, they are considered the **same origin**.

---

## Cross-Origin Example

```text
Frontend:
http://localhost:5173

Backend:
http://localhost:3001
```

The ports are different:

```text
5173 ≠ 3001
```

Therefore:

```text
Different Port
      ↓
Different Origin
      ↓
Cross-Origin Request
```

> [!important]  
> ==Even when the domain is the same, a different port means a different origin.==

---

# 11. CORS Example

Consider:

```text
Frontend:
http://localhost:5173

Backend:
http://localhost:3001
```

The frontend sends:

```http
GET /users
```

The backend can respond with a CORS header such as:

```http
Access-Control-Allow-Origin: http://localhost:5173
```

The browser checks this response header.

### Flow

```text
Frontend
http://localhost:5173
        │
        │ GET /users
        ↓
     Backend
http://localhost:3001
        │
        │ Response
        │
        │ Access-Control-Allow-Origin:
        │ http://localhost:5173
        ↓
     Browser
        │
        ↓
     Allowed
```

> [!important]  
> **CORS is enforced by the browser.**
> 
> The browser checks whether the server has permitted the requesting origin.

---

# 12. Simple Request

A **simple request** is a cross-origin request that satisfies certain browser-defined conditions.

When a request qualifies as a simple request, the browser can send the actual request **without first sending a preflight OPTIONS request**.

> [!important]  
> ==Simple request → No preflight OPTIONS request is required.==

### Example Flow

```text
React App
   ↓
GET /users
   ↓
Backend
   ↓
Response
   ↓
Access-Control-Allow-Origin
   ↓
Browser checks header
   ↓
Allowed
```

---

# 13. Preflight Request

A **preflight request** is a preliminary request made by the browser before sending certain cross-origin requests.

The browser sends an:

```http
OPTIONS
```

request first.

### Example

```http
OPTIONS /users
```

The browser asks the server whether the actual request is allowed.

For example, the actual request might contain:

```http
POST /users
Content-Type: application/json
Authorization: Bearer xyz
```

These request characteristics can cause the browser to perform a preflight request.

> [!important]  
> ==Preflight request = Browser sends OPTIONS first to check whether the actual cross-origin request is permitted.==

---

# 14. Simple Request vs Preflight Request

### Simple Request

```text
Browser
   ↓
Actual Request
   ↓
Server
   ↓
Response
```

### Preflight Request

```text
Browser
   ↓
OPTIONS
   ↓
Server
   ↓
Permission
   ↓
Actual Request
   ↓
Server
   ↓
Response
```

> [!tip]  
> **Interview Shortcut**
> 
> **Simple Request**
> 
> `Browser → Actual Request → Server`
> 
> **Preflight Request**
> 
> `Browser → OPTIONS → Server → Actual Request → Server`

---

# 15. CORS — Important Headers

Some important CORS-related headers include:

### `Access-Control-Allow-Origin`

Specifies which origin is allowed to access the resource.

```http
Access-Control-Allow-Origin: http://localhost:5173
```

### `Access-Control-Allow-Methods`

Specifies which HTTP methods are allowed.

```http
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
```

### `Access-Control-Allow-Headers`

Specifies which request headers are allowed.

```http
Access-Control-Allow-Headers: Content-Type, Authorization
```

---

# 16. Complete CORS Flow

```text
React / Frontend
http://localhost:5173
        │
        │ Cross-Origin Request
        ↓
Backend
http://localhost:3001
        │
        │
        ├── Simple Request
        │       ↓
        │   Actual Response
        │
        └── Preflight Required
                ↓
             OPTIONS
                ↓
             Backend
                ↓
        Permission / CORS Headers
                ↓
          Actual Request
                ↓
             Response
                ↓
             Browser
```

---

# 17. Quick Revision

## Persistent Connection

> ==Same TCP connection can be reused for multiple HTTP requests.==

```text
Connect → Req 1 → Res 1 → Req 2 → Res 2 → Req 3 → Res 3 → Disconnect
```

---

## Multiplexing

> ==Multiple HTTP requests/responses can travel over the same TCP connection.==

```text
Request 1 ─┐
Request 2 ─┼──→ Same TCP Connection
Request 3 ─┘
```

---

## HTTP Headers

> ==Headers provide metadata/information about an HTTP message.==

```text
HTTP Message
├── Headers
└── Body
```

---

## HTTP Methods

|Method|Main Purpose|
|---|---|
|GET|Retrieve|
|POST|Submit/Create|
|PUT|Replace/Create|
|PATCH|Partial Update|
|DELETE|Remove|
|HEAD|Headers only|
|OPTIONS|Supported methods/options|
|TRACE|Diagnostic|
|CONNECT|Establish tunnel|

---

## Idempotency

```text
Idempotent
├── GET
├── PUT
├── DELETE
├── HEAD
└── OPTIONS

Non-Idempotent
├── POST
└── PATCH
```

---

## CORS

> ==CORS controls cross-origin resource access in browsers.==

```text
Origin = Protocol + Domain + Port
```

Example:

```text
http://localhost:5173
              ↓
        Different port
              ↓
http://localhost:3001
              ↓
       Cross-Origin
```

---

## Simple vs Preflight

```text
Simple Request
Browser → Actual Request → Server


Preflight Request
Browser → OPTIONS → Server
                    ↓
              Permission
                    ↓
          Actual Request
```

> [!important]
> 
> ### 🔥 Interview Points to Remember
> 
> 1. **Persistent connection** → Reuses the same TCP connection.
>     
> 2. **Multiplexing** → Multiple requests/responses share the same TCP connection.
>     
> 3. **HTTP headers** → Metadata about the HTTP message.
>     
> 4. **GET, PUT, DELETE, HEAD, OPTIONS** → Idempotent.
>     
> 5. **POST** → Non-idempotent.
>     
> 6. **CORS** → Cross-Origin Resource Sharing.
>     
> 7. **Origin** → Protocol + Domain + Port.
>     
> 8. **Different port = different origin.**
>     
> 9. **Preflight request uses OPTIONS.**
>     
> 10. **CORS is enforced by the browser.**
>     
> 11. **Client does not directly access the database.**
>     
> 12. **Nginx can act as a reverse proxy between the client and backend server.**
>
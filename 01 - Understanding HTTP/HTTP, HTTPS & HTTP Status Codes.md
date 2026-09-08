
> [!important]  
> ==HTTP is the protocol used for communication between a client and server.==
> 
> ==HTTPS = HTTP + TLS security.==

---

# 1. HTTP Flow

A typical HTTP request flow can involve **preflight checking**, the actual request, and a response.

```text
Browser
   ↓
OPTIONS Request
(Preflight / Headers)
   ↓
Backend
   ↓
Allowed?
   ↓ Yes
POST Request
   ↓
Backend
   ↓
Response
```

> [!note]  
> The `OPTIONS` request shown above is typically a **CORS preflight request**. It is not required for every HTTP request.

### Example

```text
Browser
   ↓
OPTIONS /users
   ↓
Backend checks CORS rules
   ↓
Allowed
   ↓
POST /users
   ↓
Backend processes request
   ↓
Response
```

---

# 2. HTTP Response Status Codes

HTTP status codes tell the client **what happened to its request**.

They are divided into **five categories**:

|Code|Category|Meaning|
|---|---|---|
|`1xx`|Information|Request received / processing information|
|`2xx`|Success|Request was successfully processed|
|`3xx`|Redirection|Further action or cached representation may be used|
|`4xx`|Client Error|Problem with the request/client side|
|`5xx`|Server Error|Server failed to successfully handle the request|

> [!important]  
> ==The first digit tells you the general category of the response.==
> 
> `2xx` → Success  
> `4xx` → Client-side/request error  
> `5xx` → Server-side error

---

# 3. Mostly Used HTTP Status Codes

## 3.1 `2xx` — Success

### `200 OK`

The request was successfully processed.

```text
GET /users
        ↓
200 OK
```

> [!tip]  
> **Interview:** `200` generally means **successful request**.

---

### `201 Created`

A new resource was successfully created.

```text
POST /users
        ↓
201 Created
```

> [!important]  
> ==Use `201 Created` when a request successfully creates a new resource.==

---

### `204 No Content`

The request was successfully processed, but there is **no response body** to return.

```text
DELETE /users/10
        ↓
204 No Content
```

> [!tip]  
> **Interview:** `204` = Success + **no response body**.

---

# 4. `3xx` — Redirection

## `301 Moved Permanently`

The resource has been **permanently moved** to another URL.

```text
Old URL
   ↓
301
   ↓
New URL
```

---

## `302 Found`

The resource is **temporarily available at another URL**.

> [!note]  
> `302` indicates a temporary redirect. The exact behavior of clients can vary, especially around how methods are handled.

---

## `304 Not Modified`

The requested resource has **not changed since the client's cached version**.

```text
Client Cache
    ↓
Request with cache validator
    ↓
Server
    ↓
304 Not Modified
    ↓
Use cached version
```

> [!important]  
> ==`304` is closely related to HTTP caching and tells the client that its cached representation can still be used.==

---

# 5. `4xx` — Client Errors

`4xx` responses indicate that the request cannot be successfully processed because of something related to the request.

---

## `400 Bad Request`

The server cannot process the request because the request is invalid or malformed.

```text
Invalid Request
      ↓
400 Bad Request
```

### Example

```json
{
  "email": "invalid-email"
}
```

---

## `401 Unauthorized`

The request requires valid authentication credentials, but the client has not provided valid authentication.

```text
No valid authentication
          ↓
       401
```

> [!important]  
> ==401 → Authentication problem==
> 
> Think: **"Who are you?"**

---

## `403 Forbidden`

The server understood the request, but **refuses to allow access**.

```text
Authenticated User
        ↓
Insufficient Permission
        ↓
403 Forbidden
```

> [!important]  
> ==403 → Authorization / permission problem==
> 
> Think: **"I know who you are, but you are not allowed to do this."**

### Easy Interview Difference

```text
401 → Authentication problem
403 → Authorization problem
```

---

## `404 Not Found`

The requested resource could not be found.

```text
GET /users/999
        ↓
404 Not Found
```

---

## `405 Method Not Allowed`

The HTTP method is known by the server, but it is **not supported for that particular resource**.

```text
DELETE /users
        ↓
DELETE not allowed
        ↓
405 Method Not Allowed
```

---

## `409 Conflict`

The request conflicts with the current state of the resource.

A common example is attempting to create a resource that would violate a uniqueness constraint.

```text
POST /users
Email already exists
        ↓
409 Conflict
```

> [!tip]  
> `409` is commonly used for **duplicate/conflicting resources**, but it is not limited only to duplicates.

---

## `429 Too Many Requests`

The client has sent **too many requests in a given period of time**.

```text
Client
 ↓
Request
Request
Request
Request
Request
 ↓
429 Too Many Requests
```

> [!important]  
> ==`429` is commonly returned when rate limiting is triggered.==

---

# 6. `5xx` — Server Errors

`5xx` responses indicate that the server failed to successfully fulfill an apparently valid request.

---

## `500 Internal Server Error`

A generic server-side error occurred.

```text
Request
   ↓
Server Error
   ↓
500 Internal Server Error
```

> [!important]  
> ==`500` is a general-purpose server error.==

---

## `501 Not Implemented`

The server does not support the functionality required to fulfill the request.

> [!note]  
> It can indicate that the server does not recognize or support the requested functionality.

---

## `502 Bad Gateway`

A server acting as a **gateway or proxy** received an invalid response from an upstream server.

```text
Client
   ↓
Nginx / Proxy
   ↓
Node.js
   ↓
Invalid / unexpected response
   ↓
502 Bad Gateway
```

> [!important]  
> ==`502` commonly appears when a proxy or gateway cannot get a valid response from an upstream server.==

---

## `503 Service Unavailable`

The server is currently unable to handle the request.

Possible reasons:

- Server is overloaded
    
- Server is temporarily down
    
- Maintenance is happening
    
- Required service is unavailable
    

```text
Request
   ↓
Server unavailable
   ↓
503 Service Unavailable
```

---

## `504 Gateway Timeout`

A gateway or proxy did not receive a timely response from an upstream server.

```text
Client
   ↓
Nginx
   ↓
Node.js
   ↓
Too Slow / No Response
   ↓
504 Gateway Timeout
```

> [!important]  
> ==502 → Invalid upstream response==
> 
> ==504 → Upstream response took too long / timed out==

---

# 7. HTTP Status Code Quick Reference

|Status|Name|Common Meaning|
|--:|---|---|
|`200`|OK|Request successful|
|`201`|Created|Resource created|
|`204`|No Content|Success, no response body|
|`301`|Moved Permanently|Permanent redirect|
|`302`|Found|Temporary redirect|
|`304`|Not Modified|Use cached representation|
|`400`|Bad Request|Invalid/malformed request|
|`401`|Unauthorized|Authentication required/failed|
|`403`|Forbidden|Access not permitted|
|`404`|Not Found|Resource not found|
|`405`|Method Not Allowed|HTTP method not allowed|
|`409`|Conflict|Request conflicts with resource state|
|`429`|Too Many Requests|Rate limit exceeded|
|`500`|Internal Server Error|General server error|
|`501`|Not Implemented|Functionality not supported|
|`502`|Bad Gateway|Invalid upstream response|
|`503`|Service Unavailable|Server/service temporarily unavailable|
|`504`|Gateway Timeout|Upstream server timed out|

---

# 8. HTTP Caching

> [!important]  
> ==HTTP caching means storing a copy of an HTTP response so that future requests can reuse the stored representation instead of always retrieving it again from the origin server.==

### Basic Flow

```text
First Request
     ↓
   Server
     ↓
  Response
     ↓
 Cache stores response
     ↓
Future Request
     ↓
Use / validate cached response
```

Caching can improve:

- **Performance**
    
- **Response time**
    
- **Network efficiency**
    
- **Server load**
    

---

# 9. `no-cache` vs `no-store`

These are `Cache-Control` directives.

## `Cache-Control: no-cache`

> [!important]  
> ==`no-cache` does NOT mean "do not store".==
> 
> It means a cached response must be **revalidated with the server before reuse**.

```text
no-cache
   ↓
Can store response
   ↓
Must revalidate before reuse
```

---

## `Cache-Control: no-store`

> [!important]  
> ==`no-store` tells caches not to store the response.==

```text
no-store
   ↓
Do not store the response
```

### Interview Difference

|Directive|Can Store?|Revalidation|
|---|---|---|
|`no-cache`|Yes|Required before reuse|
|`no-store`|No|Not applicable|

> [!tip]  
> **Remember:**
> 
> `no-cache` ≠ Don't cache  
> `no-store` = Don't store

---

# 10. SSL, TLS & HTTPS

## SSL

**SSL = Secure Sockets Layer**

SSL was the original protocol used to provide secure communication over networks.

> [!note]  
> Modern systems use **TLS**, not the old SSL versions.

---

## TLS

**TLS = Transport Layer Security**

TLS is the modern successor to SSL and provides security features such as:

- Encryption
    
- Integrity protection
    
- Server authentication
    

> [!important]  
> ==TLS protects data while it is being transmitted between communicating endpoints.==

---

## HTTPS

**HTTPS = HTTP Secure**

HTTPS means HTTP communication is protected using **TLS**.

```text
HTTPS
  =
HTTP
 +
TLS
```

> [!important]  
> ==HTTPS is not a completely different application protocol from HTTP; it is HTTP secured using TLS.==

---

# 11. HTTP + TLS + TCP

For a traditional HTTP/1.1 or HTTP/2 connection over TCP:

```text
HTTP
  ↓
Application Protocol
  ↓
TLS
  ↓
Security / Encryption
  ↓
TCP
  ↓
Reliable Transport
```

### Simple Understanding

```text
HTTP → Defines the request/response communication
TLS  → Provides security
TCP  → Provides reliable transport
```

> [!important]  
> ==HTTP defines how the client and server communicate.==
> 
> ==TLS secures that communication.==
> 
> ==TCP provides reliable transport for traditional HTTPS over TCP.==

> [!note]  
> HTTP/3 uses **QUIC over UDP** instead of TCP, so the TCP part applies to traditional HTTP versions such as HTTP/1.1 and HTTP/2.

---

# 12. Final Backend Architecture

A common production-style architecture can look like this:

```text
                    INTERNET
                       │
                       ▼
                   🌐 Browser
                       │
                       │ HTTPS
                       ▼
                 ┌───────────┐
                 │   Nginx   │
                 │           │
                 │ TLS       │
                 │ Termination
                 │ Reverse   │
                 │ Proxy     │
                 └─────┬─────┘
                       │
                       │ HTTP
                       │ Internal Communication
                       ▼
              ┌─────────────────┐
              │ Node.js /       │
              │ Express Backend  │
              └────────┬────────┘
                       │
                       │ Database Query
                       ▼
              ┌─────────────────┐
              │    Database     │
              └─────────────────┘
```

---

# 13. Architecture Flow Explained

### Step 1 — Browser

The user sends a request from the browser.

```text
Browser
   ↓
HTTPS Request
```

---

### Step 2 — Nginx

Nginx receives the HTTPS request.

It can perform tasks such as:

- **TLS termination**
    
- Reverse proxying
    
- Load balancing
    
- Request routing
    

```text
Browser
   ↓ HTTPS
Nginx
```

---

### Step 3 — TLS Termination

Nginx can handle the TLS connection and decrypt the HTTPS traffic before forwarding the request internally.

```text
HTTPS
  ↓
Nginx
  ↓
TLS termination
  ↓
HTTP request
```

> [!important]  
> ==TLS termination means the TLS-protected connection from the client is terminated at the proxy/server, where the encrypted traffic is decrypted.==

---

### Step 4 — Node.js / Express

Nginx forwards the request to the Node.js/Express application.

```text
Nginx
   ↓
HTTP
   ↓
Node.js / Express
```

The backend processes:

- Routing
    
- Authentication
    
- Authorization
    
- Validation
    
- Business logic
    
- Database operations
    

---

### Step 5 — Database

The Node.js application communicates with the database.

```text
Node.js
   ↓
Database Query
   ↓
Database
   ↓
Database Result
   ↓
Node.js
```

---

### Step 6 — Response

The response travels back through the architecture.

```text
Database
   ↓
Node.js
   ↓
Nginx
   ↓
HTTPS
   ↓
Browser
```

### Complete Flow

```text
Browser
   ↓
HTTPS
   ↓
Nginx
   ↓
HTTP (internal)
   ↓
Node.js / Express
   ↓
Database
   ↓
Node.js / Express
   ↓
Nginx
   ↓
HTTPS
   ↓
Browser
```

---

# 14. Interview Important Points ⭐

> [!important]
> 
> ### ⭐ Remember These
> 
> **HTTP**
> 
> - Request/response protocol
>     
> - Stateless at the protocol level
>     
> 
> **HTTPS**
> 
> - HTTP + TLS
>     
> 
> **TLS**
> 
> - Provides encryption, integrity, and authentication
>     
> 
> **`200`**
> 
> - Successful request
>     
> 
> **`201`**
> 
> - Resource created
>     
> 
> **`204`**
> 
> - Success with no response body
>     
> 
> **`301`**
> 
> - Permanent redirect
>     
> 
> **`304`**
> 
> - Cached representation can still be used
>     
> 
> **`400`**
> 
> - Bad request
>     
> 
> **`401`**
> 
> - Authentication problem
>     
> 
> **`403`**
> 
> - Authorization/access problem
>     
> 
> **`404`**
> 
> - Resource not found
>     
> 
> **`409`**
> 
> - Resource/state conflict
>     
> 
> **`429`**
> 
> - Too many requests / rate limiting
>     
> 
> **`500`**
> 
> - Internal server error
>     
> 
> **`502`**
> 
> - Bad response from upstream server
>     
> 
> **`503`**
> 
> - Service temporarily unavailable
>     
> 
> **`504`**
> 
> - Gateway timed out waiting for upstream server
>     
> 
> **`no-cache`**
> 
> - Can store, but must revalidate before reuse
>     
> 
> **`no-store`**
> 
> - Do not store
>     
> 
> **Nginx**
> 
> - Can act as a reverse proxy and perform TLS termination
>     
> 
> **TLS Termination**
> 
> - TLS connection is terminated/decrypted at the proxy/server
>     

---

# 15. One-Line Mental Model

```text
HTTP       → Communication
HTTPS      → Secure HTTP
TLS        → Security
Status     → Result of the request
Caching    → Reuse stored responses
Nginx      → Reverse Proxy
Node.js    → Backend Application
Database   → Persistent Data
```

> [!tip]
> 
> ### 🧠 Backend Interview Shortcut
> 
> **Browser → HTTPS → Nginx → Node.js → Database**
> 
> Think:
> 
> **HTTPS = Security**  
> **Nginx = Gateway/Reverse Proxy**  
> **Node.js = Business Logic**  
> **Database = Data**
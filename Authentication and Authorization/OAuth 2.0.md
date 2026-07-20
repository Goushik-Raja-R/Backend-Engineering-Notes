
## Definition

OAuth 2.0 is an **authorization framework** that allows users to grant limited access to their resources without sharing their passwords.

> OAuth 2.0 = Authorization using Access Tokens.

---

## Why OAuth 2.0 was introduced

OAuth 1.0 was secure but complicated.

OAuth 2.0 simplified the process by:
- Using HTTPS instead of signing every request.
- Introducing Refresh Tokens.
- Supporting multiple authorization flows.

---

## Flow (Authorization Code Flow)

```text
User
   │
   ▼
Client Application
   │
Redirect
   ▼
Authorization Server
   │
Login + Consent
   ▼
Authorization Code
   │
Exchange
   ▼
Access Token
   │
   ▼
Resource Server
```

---

## Example

Continue with Google

1. User clicks "Continue with Google".
2. Google asks the user to log in.
3. Google asks:
   "Allow this application to access your profile?"
4. User clicks **Allow**.
5. Google returns an Authorization Code.
6. The client exchanges the code for an Access Token.
7. The client accesses the user's profile.

---

## Components

- Resource Owner → User
- Client → Third-party application
- Authorization Server → Google
- Resource Server → Google API
- Access Token
- Refresh Token

---

## Tokens

### Access Token

- Short-lived
- Used to access protected resources

### Refresh Token

- Long-lived
- Used to obtain a new Access Token without asking the user to log in again

---

## Advantages

- Simple to implement
- Widely adopted
- Secure over HTTPS
- Supports mobile, web, and APIs
- Supports Refresh Tokens

---

## Interview Definition

> OAuth 2.0 is an authorization framework that enables users to grant limited access to their resources using access tokens without sharing their passwords.

---

## One-Line Note

> OAuth 2.0 = Authorization framework that uses Access Tokens and HTTPS to provide secure delegated access.
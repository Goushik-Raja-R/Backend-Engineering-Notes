
## Definition

OAuth 1.0 is an **authorization protocol** that allows a third-party application to access a user's resources without sharing the user's password.

> OAuth 1.0 = Authorization without sharing passwords.

---

## Why OAuth 1.0 was introduced

Before OAuth:

```text
User
   │
Username + Password
   ▼
Third-Party App
```

Problems:
- Password is shared with the third-party app.
- If the app is compromised, the user's account is at risk.
- The app gets full access to the account.

OAuth 1.0 solves this by issuing an **Access Token** instead of sharing the password.

---

## Flow

```text
User
   │
   ▼
Client Application
   │
Requests Permission
   ▼
Authorization Server
   │
User Login + Consent
   ▼
Access Token
   │
   ▼
Client
   │
Uses Token
   ▼
Resource Server
```

---

## Example

PhotoPrint App wants to access your Facebook photos.

1. PhotoPrint asks for permission.
2. You are redirected to Facebook.
3. You log in.
4. Facebook asks:
   "Allow PhotoPrint to access your photos?"
5. You click **Allow**.
6. Facebook issues an Access Token.
7. PhotoPrint accesses only your photos.

---

## Security

OAuth 1.0 secures every API request using **cryptographic signatures**.

This prevents:
- Request tampering
- Replay attacks

---

## Advantages

- Password is never shared.
- Secure request signing.
- Limited resource access.

---

## Disadvantages

- Complex implementation.
- Every request must be signed.
- Difficult to develop and maintain.

---

## Interview Definition

> OAuth 1.0 is an authorization protocol that allows third-party applications to access user resources without sharing passwords by using cryptographically signed requests and access tokens.

---

## One-Line Note

> OAuth 1.0 = Authorization protocol that uses cryptographic signatures to securely grant limited access without sharing passwords.
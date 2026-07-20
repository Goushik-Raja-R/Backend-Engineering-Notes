# OpenID Connect 

## Definition

OpenID Connect (OIDC) is an **authentication protocol** built on top of OAuth 2.0.

> OAuth tells **what the application can access**.
>
> OpenID Connect tells **who the user is**.

---

## Why OpenID Connect was introduced

OAuth 2.0 provides authorization only.

Applications also needed a standard way to:
- Verify user identity
- Get basic user information

OpenID Connect solves this problem.

---

## Flow

```text
User
   │
   ▼
Client Application
   │
Redirect
   ▼
Identity Provider
(Google)
   │
Login + Consent
   ▼
Authorization Code
   ▼
Client
   │
Exchange
   ▼
Access Token
+
ID Token
```

---

## ID Token

An ID Token is a JWT that contains information about the authenticated user.

Example information:
- User ID
- Name
- Email
- Email Verified
- Profile Picture

---

## Example

Continue with Google

1. User clicks "Continue with Google".
2. Google authenticates the user.
3. Google returns:
   - Access Token
   - ID Token
4. The application reads the ID Token to identify the user.

---

## Components

- Identity Provider (Google)
- Client Application
- User
- ID Token
- Access Token

---

## OAuth vs OpenID Connect

| OAuth 2.0 | OpenID Connect |
|------------|----------------|
| Authorization | Authentication |
| Access Token | ID Token + Access Token |
| Resource access | User identity |
| "What can this app access?" | "Who is the user?" |

---

## Advantages

- Standard authentication protocol
- Supports Single Sign-On (SSO)
- Uses JWT ID Tokens
- Built on OAuth 2.0

---

## Interview Definition

> OpenID Connect is an authentication protocol built on top of OAuth 2.0 that verifies user identity using an ID Token while still supporting OAuth authorization.

---

## One-Line Note

> OpenID Connect = Authentication layer built on OAuth 2.0 that identifies the user using an ID Token.
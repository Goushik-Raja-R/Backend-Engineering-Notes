# Define

- **Authentication = who are you**
- **Authorization = what can you do**

# Historical Origin

- **In back days if the village is there means the person who won the trust with the people will vouch for someone so that the will offer in something to that person `old days authentication`.**
  
- **The above one will be applicable only for the village what will happen if the person will go outside of the village that it will not work for that only the  next step they have gone to [[Seal Based Authentication]]**

 - **But this methods are being easily attacked by [[Bypass Attacks]]**

 - **Later than Telegraph came it will share the pass phrase with one another.**
   
   

   
  # **After industrial Revolution**
  
 -   **`from something you possessed to something you know 
 
  # Computation
  
-  **The first computer password system was introduced in 1961 in MIT's Compatible Time-Sharing System (CTSS) to protect users' files on a shared mainframe computer.
  
- **Before time-sharing systems, one person typically used a computer at a time, so passwords weren't necessary. Once multiple users shared the same computer, a way to identify and protect each user's files became essential [[password-related security incidents 1961]].
  
  
  # Hashing 
  
  - **Hashing is one of the most important authentication topics for backend engineers because it's used to securely store passwords.**
  
  `*example*`
```
		```Password:
			Captain123
		
				↓
		
			Hash Function
		
				↓
		
			8d969eef6ecad3c29a3a629280e686cf...
```

# Encryption

- **Encryption is the process of converting readable data (plaintext) into an unreadable format (ciphertext) using an encryption algorithm and a key.**
  
  `example`
	  
	  Plaintext:Captain123
		
		     ↓
		
		Encryption + Key
		
		     ↓
		
		Ciphertext:
		X7@k9LmP#2q


# Types of encryption

  [[Symmetric Encryption]]
  [[Asymmetric Encryption]]
  
  
# Decryption

- **Decryption is the process of converting encrypted data (ciphertext) back into its original readable form (plaintext) using the correct key.**
  
  
  [[Hashing vs Encryption]]
  
# Remember these three together:

- **Hashing** → Store passwords securely (bcrypt, Argon2).
- **Encryption** → Protect sensitive data that must be read later (credit card numbers, API secrets).
- **TLS/HTTPS** → Encrypts data **while it's traveling over the network** between the client and server.
  
  
# Security
 
-  **C** → **Confidentiality**
-  **I** → **Integrity**
-  **A** → **Availability**

  
-  **Confidentiality:** Ensures that only authorized users can access or read data.
-  **Integrity:** Ensures that data remains accurate and unmodified by unauthorized users.
-  **Availability:** Ensures that systems and data are accessible to authorized users whenever needed.
  
  
# MFA

- **Multi-Factor Authentication (MFA) is a security process that requires two or more different authentication factors to verify a user's identity.**

  [[MFA Three Authentication Factors]]

# Session

- **A session stores information about a logged-in user between multiple HTTP requests.**

Remember:

> **HTTP is stateless.**

So after login, the server needs a way to remember the user.


# Session Persistence?

- **Session Persistence means storing session data somewhere so it survives across multiple requests and can be accessed by the server.**

**There are three common options.**

- [[Memory store]]
-  [[Redis store - Remote Dictionary Server]]
-  [[Database store]]
  
  `example`

	**Node.js Memory**
	
	- **Teacher A → Notebook A**
	- **Teacher B → Notebook B**
	
	**Redis**
	
			Teacher A
		       │
			Teacher B
		       │
			Teacher C
		       ▼
		Central Register (Redis)


# **Types of Authentication**

- # **[[Json Web Token]]**

- # **[[Session]]**

- # **[[API Key]]**

- # **[[OAuth 1.0]]**

- # **[[OAuth 2.0]]**

- # **[[OIDC]]**
  
  
# #**Which auth to choose?**

- # **[[Stateful]]**

- # **[[Stateless]]**

- # **[[OAuth]]**

- # **[[API key auth]]**
  
  
  ---
  

# Authorization
# [[RBAC]]
  

---
# Authentication Security Best Practices

# [[Error Message]]

# [[Timing Attacks]]
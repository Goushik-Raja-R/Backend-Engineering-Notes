# Role-Based Access Control 

## Definition

**Role-Based Access Control (RBAC)** is an authorization mechanism where permissions are assigned to **roles**, and users receive permissions by being assigned those roles.

> **Authorization means giving specific permissions to a specific user on a specific platform or resource.**

---

# Why RBAC?

Instead of assigning permissions to every user individually, permissions are assigned to roles.

This makes user management:
- Easier
- More secure
- Scalable

---

# How RBAC Works

```text
User
   │
Assigned Role
   ▼
Role
   │
Has Permissions
   ▼
Resources
```

---

# Flow

```text
User Login
      │
      ▼
Authentication
(Who are you?)
      │
      ▼
Authorization (RBAC)
(What can you do?)
      │
      ▼
Role Checked
      │
      ▼
Allow / Deny Access
```

---

# Example

Suppose an employee management system has three roles.

### Admin

Permissions:
- Create Employee
- Update Employee
- Delete Employee
- View Employee

---

### Manager

Permissions:
- Create Employee
- Update Employee
- View Employee

Cannot:
- Delete Employee

---

### Employee

Permissions:
- View Own Profile
- Update Own Profile

Cannot:
- Create Employees
- Delete Employees

---

# Real-World Example

## Banking Application

### Customer

- View Account
- Transfer Money
- Download Statement

---

### Bank Employee

- View Customer Accounts
- Approve Requests

---

### Bank Manager

- Approve Loans
- Manage Employees
- Generate Reports

Each role has different permissions.

---

# Node.js Example

```javascript
function authorize(...roles) {
    return (req, res, next) => {
        if (!roles.includes(req.user.role)) {
            return res.status(403).json({
                message: "Access Denied"
            });
        }

        next();
    };
}
```

Usage:

```javascript
router.delete(
    "/employee/:id",
    authenticate,
    authorize("ADMIN"),
    deleteEmployee
);
```

Only **ADMIN** can access this API.

---

# Advantages

- Easy to manage users.
- Improves security.
- Reduces duplicate permission assignments.
- Easy to scale.
- Centralized permission management.

---

# RBAC in JWT

After authentication, the JWT may contain:

```json
{
    "userId": "123",
    "role": "ADMIN"
}
```

When a request arrives:

1. Verify JWT.
2. Read the user's role.
3. Check if the role has permission.
4. Allow or deny access.

---

# Authentication vs Authorization

## Authentication

> Verifies **who the user is**.

Examples:
- Password
- OTP
- Fingerprint

Question answered:

> **Who are you?**

---

## Authorization

> Gives **specific permissions to a specific user on a specific platform or resource.**

Question answered:

> **What are you allowed to do?**

---

# Interview Definition

> **RBAC (Role-Based Access Control) is an authorization model where permissions are assigned to roles instead of individual users. Users inherit permissions through their assigned roles, making access management simpler, more secure, and scalable.**

---

# One-Line Notes

- **RBAC = Users are assigned roles, and roles determine permissions.**
- **Authentication = Verifies the user's identity.**
- **Authorization = Gives specific permissions to a specific user on a specific platform or resource.**

> [!info] Definition  
> **Custom action APIs** are endpoints used when we want to perform a specific business action on the server that does not naturally fit into the standard CRUD operations.

### CRUD Operations

```text
Create → POST
Read   → GET
Update → PUT / PATCH
Delete → DELETE
```

Sometimes an operation does not clearly represent:

- Creating a resource
    
- Reading a resource
    
- Updating a resource
    
- Deleting a resource
    

In such cases, we can design a **custom action endpoint**.

---

# Why Use POST?

`POST` is commonly used for custom actions because it can represent an operation that **causes a server-side action or state change**.

> [!important]  
> `POST` is **not limited to creating resources**.
> 
> It can also be used to trigger a business action or process on the server.

---

# Examples

### Cancel an Order

Instead of trying to represent cancellation as a normal CRUD operation:

```http
POST /orders/101/cancel
```

Meaning:

> Perform the `cancel` action on Order `101`.

---

### Approve an Organization

```http
POST /organizations/101/approve
```

Meaning:

> Perform the `approve` action on Organization `101`.

---

### Send Password Reset Email

```http
POST /users/101/send-password-reset
```

Meaning:

> Trigger the password-reset email process for User `101`.

---

### Custom Action Flow

```text
Client
   ↓
POST /orders/101/cancel
   ↓
Server
   ↓
Validate request
   ↓
Execute business logic
   ↓
Update database
   ↓
Return response
```

---

# Why Not GET?

`GET` is intended for **retrieving data**.

A custom action usually performs some operation or causes a state change, so `GET` should not normally be used.

❌ Avoid:

```http
GET /orders/101/cancel
```

✅ Prefer:

```http
POST /orders/101/cancel
```

---

# Why Not PUT / PATCH?

`PUT` and `PATCH` are primarily used when we are **updating the representation/state of a resource**.

For example:

```http
PATCH /orders/101
```

```json
{
  "status": "cancelled"
}
```

This can be appropriate if cancellation is simply a normal state update.

But if cancellation involves **business logic or multiple operations**, a custom action can be clearer:

```http
POST /orders/101/cancel
```

For example:

```text
Cancel Order
     ↓
Change order status
     ↓
Release inventory
     ↓
Cancel payment authorization
     ↓
Send notification
```

Here, `cancel` is more than simply changing one field.

---

# Important Understanding

> [!important]  
> **Use normal CRUD endpoints when the operation naturally maps to CRUD.**
> 
> **Use a custom action endpoint when the operation represents a specific business action that doesn't naturally fit CRUD.**

### Example

Normal update:

```http
PATCH /orders/101
```

```json
{
  "shippingAddress": "New Address"
}
```

Custom business action:

```http
POST /orders/101/cancel
```

---

# Easy Way to Remember

```text
Does the operation naturally fit CRUD?
             ↓
          YES
             ↓
       Use CRUD API


Does it represent a specific business action?
             ↓
           YES
             ↓
     Consider POST /resource/{id}/action
```

### One-Line Interview Answer

> **Custom action APIs are used for business operations that don't naturally fit CRUD, and `POST` is commonly used to trigger these server-side actions.**
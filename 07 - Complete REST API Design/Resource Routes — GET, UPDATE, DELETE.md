
## Same Route, Different HTTP Methods

For a specific organization, the route can look the same for different operations:

```http
GET    http://localhost:3000/organizations/101
PATCH  http://localhost:3000/organizations/101
DELETE http://localhost:3000/organizations/101
```

The **HTTP method determines what operation is performed**.

|Method|Endpoint|Purpose|
|---|---|---|
|`GET`|`/organizations/{id}`|Get a specific organization|
|`PATCH`|`/organizations/{id}`|Partially update an organization|
|`DELETE`|`/organizations/{id}`|Delete an organization|

> [!important]  
> The **path identifies the resource**, while the **HTTP method defines the operation**.

### Example

```http
GET /organizations/101
```

→ Get Organization `101`

```http
PATCH /organizations/101
```

→ Update Organization `101`

```http
DELETE /organizations/101
```

→ Delete Organization `101`

---

# HTTP 404 — Not Found

> [!info] Definition  
> `404 Not Found` is generally returned when the server cannot find the **specific resource requested by the client**.

### Example

Suppose these organizations exist:

```text
Organization 101
Organization 102
Organization 103
```

The client requests:

```http
GET /organizations/999
```

If Organization `999` does not exist:

```http
404 Not Found
```

Because the client specifically requested **Organization 999**, and that resource does not exist.

---

# GET Collection With No Data

Consider:

```http
GET /organizations
```

This request asks for the **collection of organizations**, not a specific organization.

If there are currently no organizations, the API can return:

```http
200 OK
```

with:

```json
{
  "data": []
}
```

> [!important]  
> An empty collection is usually **not an error**. The collection exists; it simply contains zero resources.

### Compare

#### Collection exists but is empty

```http
GET /organizations
```

Response:

```http
200 OK
```

```json
{
  "data": []
}
```

#### Specific resource does not exist

```http
GET /organizations/999
```

Response:

```http
404 Not Found
```

---

# Easy Way to Remember

```text
GET /organizations
        ↓
"Give me the organizations"
        ↓
No organizations?
        ↓
200 OK + empty array
```

```text
GET /organizations/999
        ↓
"Give me Organization 999"
        ↓
Doesn't exist?
        ↓
404 Not Found
```

> [!tip] Interview Shortcut  
> **Empty collection → Usually `200 OK` with `[]`**
> 
> **Specific resource doesn't exist → Usually `404 Not Found`**

---

# Important Correction to My Understanding

❌ **Not exactly correct:**

> "`404` only happens when the client asks for particular data."

✅ **Better understanding:**

> `404 Not Found` means the server could not find the requested resource. For REST APIs, it is commonly used when a specific resource identified by the URL does not exist.

Also remember that the exact status code can depend on the API's design and the situation. The key distinction here is:

```text
Collection exists, but has no items
        ↓
200 OK + empty collection


Specific resource doesn't exist
        ↓
404 Not Found
```
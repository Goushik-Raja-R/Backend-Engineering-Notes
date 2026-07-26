
## Resources

> [!info] Definition  
> **Resources** are the main entities that the backend manages and exposes through APIs.

### Example Resources

```text
Organization
     ↓
  Project
     ↓
   Task
```

---

## REST API Endpoints

### Organization APIs

|HTTP Method|Endpoint|Purpose|
|---|---|---|
|`GET`|`/organizations`|Retrieve all organizations|
|`POST`|`/organizations`|Create a new organization|
|`GET`|`/organizations/{id}`|Retrieve a specific organization|
|`PATCH`|`/organizations/{id}`|Partially update an organization|
|`DELETE`|`/organizations/{id}`|Delete an organization|

> [!important] Same URL, Different Operations  
> The same URL can perform different operations depending on the **HTTP method**.

```http
GET  /organizations
POST /organizations
```

---

# Pagination

> [!info] Definition  
> **Pagination** is the process of dividing a large amount of data into smaller pages instead of returning everything in a single response.

### Example

```http
GET /organizations?page=1&limit=10
```

- `page=1` → Current page number
    
- `limit=10` → Number of records to return per page
    

### Example

```text
100 Organizations
       ↓
   limit = 10
       ↓
10 Organizations per page
       ↓
  10 Pages
```

### Response

```json
{
  "data": [
    {
      "id": 1,
      "name": "ABC Technologies"
    }
  ],
  "total": 100,
  "page": 1,
  "totalPages": 10
}
```

|Field|Meaning|
|---|---|
|`data`|Records returned for the current page|
|`total`|Total number of matching records|
|`page`|Current page number|
|`totalPages`|Total number of pages|

---

# Query Parameters

> [!info] Definition  
> **Query parameters** are values passed in the URL after the `?` symbol. They are commonly used to control how a collection of resources is returned.

### Example

```http
GET /organizations?page=1&limit=10
```

### Structure

```text
/path?key=value&key=value
```

### Common Uses

- Pagination
    
- Sorting
    
- Filtering
    
- Searching
    

---

# Sorting

> [!info] Definition  
> **Sorting** means arranging the returned resources according to a particular field.

### Ascending Order

```http
GET /organizations?sortBy=name&sortOrder=asc
```

- `sortBy=name` → Field used for sorting
    
- `sortOrder=asc` → Ascending order
    

### Descending Order

```http
GET /organizations?sortBy=name&sortOrder=desc
```

- `asc` → Ascending
    
- `desc` → Descending
    

### Example

Initial data:

```text
Zebra
Apple
Microsoft
```

After:

```http
?sortBy=name&sortOrder=asc
```

Result:

```text
Apple
Microsoft
Zebra
```

---

# Filtering

> [!info] Definition  
> **Filtering** means returning only the resources that satisfy a particular condition.

### Example

```http
GET /organizations?status=active
```

→ Returns only organizations whose status is `active`.

### Multiple Filters

```http
GET /organizations?status=active&country=India
```

```text
status=active
      ↓
Only active organizations

country=India
      ↓
Only organizations from India
```

Both conditions are applied to the results.

---

# Path Parameters vs Query Parameters

## Path Parameters

> [!info] Definition  
> **Path parameters** are used to identify a specific resource.

### Example

```http
GET /organizations/101
```

```text
101
 ↓
Organization ID
```

### General Structure

```http
GET /organizations/{id}
```

### Example

```http
GET /organizations/101
```

→ Get the organization whose ID is `101`.

---

## Query Parameters

> [!info] Definition  
> **Query parameters** are used to control, filter, sort, search, or paginate a collection.

### Example

```http
GET /organizations?page=1&limit=10
```

→ Get the first page with 10 organizations.

Another example:

```http
GET /organizations?status=active
```

→ Get only active organizations.

---

## Difference

|Path Parameter|Query Parameter|
|---|---|
|Identifies a specific resource|Controls how a collection is returned|
|Usually required to identify the resource|Usually optional|
|`/organizations/101`|`/organizations?page=1&limit=10`|
|**WHICH resource?**|**HOW should I get the resources?**|

> [!tip] Easy Way to Remember  
> **Path Parameter → WHICH resource?**
> 
> **Query Parameter → HOW should I get the resources?**

---

# Combining Pagination + Sorting + Filtering

You can combine multiple query parameters in a single request.

```http
GET /organizations?status=active&sortBy=name&sortOrder=asc&page=1&limit=10
```

### Request Breakdown

```text
/organizations
      ↓
Resource
      ↓
status=active
      ↓
Filtering
      ↓
sortBy=name
      ↓
Sorting
      ↓
sortOrder=asc
      ↓
Ascending
      ↓
page=1
      ↓
Pagination
      ↓
limit=10
      ↓
10 records per page
```

---

# Quick Revision

> [!important] Remember These
> 
> **Path Parameter** → Identifies a specific resource
> 
> **Query Parameter** → Controls the collection response
> 
> **Pagination** → Divides large data into pages
> 
> **Sorting** → Controls the order of data
> 
> **Filtering** → Returns only matching data
> 
> **HTTP Method** → Defines the operation on the resource

---

# Interview Quick Answers

|Concept|One-Line Answer|
|---|---|
|Resource|An entity that the API manages and exposes|
|Pagination|Dividing large result sets into smaller pages|
|Query Parameter|Controls how a collection is returned|
|Sorting|Arranging resources according to a field|
|Filtering|Returning only resources matching a condition|
|Path Parameter|Identifies a specific resource|
|HTTP Method|Defines the operation performed on a resource|

## Easy Mental Model

```text
                    REST API
                       │
              ┌────────┴────────┐
              │                 │
        Path Parameter     Query Parameter
              │                 │
         WHICH one?         HOW to get?
              │                 │
       /organizations/101   ?page=1
                            ?limit=10
                            ?sortBy=name
                            ?status=active
```
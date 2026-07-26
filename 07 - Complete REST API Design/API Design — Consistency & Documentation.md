

> [!important] Most Important Takeaway  
> **Maintain consistency across your API design.**

A well-designed API should follow consistent naming conventions, response structures, HTTP methods, and endpoint patterns.

---

## Clear Field Names

> [!tip] Naming  
> Use **clear, descriptive, and non-abbreviated field names** so developers can understand the API response without guessing.

### ❌ Avoid Abbreviations

```json
{
  "orgNm": "ABC Technologies",
  "usrId": 101,
  "phNo": "9876543210"
}
```

### ✅ Prefer Clear Names

```json
{
  "organizationName": "ABC Technologies",
  "userId": 101,
  "phoneNumber": "9876543210"
}
```

### Why?

Clear names:

- Improve readability
    
- Reduce confusion
    
- Make APIs easier to integrate
    
- Make the API self-explanatory
    
- Reduce communication between frontend and backend developers
    

---

## Interactive API Documentation

> [!info] Definition  
> **Interactive API documentation** allows developers to understand and test API endpoints directly through documentation.

Examples of information that should be documented:

- Endpoint
    
- HTTP method
    
- Request parameters
    
- Request body
    
- Response structure
    
- Status codes
    
- Authentication requirements
    
- Error responses
    

### Example

```text
POST /organizations
        ↓
Request Body
        ↓
{
  "name": "ABC Technologies"
}
        ↓
Response
        ↓
201 Created
```

Interactive documentation allows frontend developers to **understand and test the API without needing to manually construct every request**.

---

## Why API Consistency Matters

```text
Consistent API Design
        ↓
Easy to Understand
        ↓
Easy to Integrate
        ↓
Fewer Mistakes
        ↓
Better Developer Experience
```

> [!important] Interview Takeaway  
> **A good API should be predictable, consistent, clearly named, and well documented so that frontend developers can integrate with it efficiently.**

### One-Line Revision

> **Maintain consistency, use clear non-abbreviated names, and provide interactive documentation for a better developer experience.**
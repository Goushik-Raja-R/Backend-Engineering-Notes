Checks whether the input **makes sense according to business rules**.

### Examples

- Age must be greater than 18.
- User email should not already exist.
- Product quantity should not exceed available stock.
- Employee ID should exist.

Example:

```json
{
  "age": 15
}
```

❌ Fails business rule (minimum age is 18).

Checks whether the data type matches what the application expects.

### Examples

Expected:

```json
{
  "age": 25
}
```

Received:

```json
{
  "age": "twenty five"
}
```

❌ Invalid type

Expected:

```typescript
age: number
```

Received:

```json
{
  "age": "25"
}
```

May require transformation before processing.
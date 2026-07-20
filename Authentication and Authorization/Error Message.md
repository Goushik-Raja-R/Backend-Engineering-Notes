
## Definition

Error messages are responses returned by an application when a request fails.

## Best Practice

Do not reveal sensitive information through error messages. Avoid messages that help attackers identify valid users or credentials.

❌ Bad Examples

- Email does not exist.
- Password is incorrect.

These messages allow attackers to determine whether an email is registered.

✅ Good Example

- Invalid email or password.

This generic message does not reveal which part of the login failed.

## Why?

Using generic error messages prevents **user enumeration attacks**, where attackers try to discover valid usernames or email addresses.

## Interview Definition

> Error messages should provide useful feedback without exposing sensitive information that could help attackers.

## One-Line Note

> Use generic error messages to prevent attackers from identifying valid users or credentials.
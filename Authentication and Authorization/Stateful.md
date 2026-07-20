
## Definition

Stateful means the server remembers information (state) about the client between requests.

## When to use

Use stateful architecture when:
- The application is small or internal.
- The server needs to maintain user sessions.
- Session data is stored on the server.

## Examples

- Banking application with server-side sessions
- Internal company applications
- Traditional web applications

> Note: Stateful systems can also be distributed, but they require session replication or sticky sessions, which adds complexity.
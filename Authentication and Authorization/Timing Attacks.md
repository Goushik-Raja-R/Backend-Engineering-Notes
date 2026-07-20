
## Definition

A timing attack is a security attack where an attacker measures the time taken by a system to respond and uses those differences to guess sensitive information like passwords, API keys, or cryptographic secrets.

## How it Works

If a system takes longer to process partially correct input than incorrect input, an attacker can measure these time differences and gradually infer the correct secret.

## Prevention

- Use constant-time comparison functions (e.g., `crypto.timingSafeEqual()` in Node.js).
- Return generic authentication error messages.
- Avoid response time differences for valid and invalid credentials.

## Interview Definition

> A timing attack is a side-channel attack that exploits response time differences to infer sensitive information.

## One-Line Note

> Timing Attack = Measuring response times to guess secret information.
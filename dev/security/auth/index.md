# Auth — Security

The place where most security mistakes happen. Not because it's hard — because people rush it or copy the wrong pattern.

---

## Sessions vs JWT — Pick the Right One

| | Sessions | JWT |
|--|---------|-----|
| Storage | Server-side (DB/Redis) | Client-side (cookie or localStorage) |
| Revocation | Instant — delete the session | Hard — token lives until expiry |
| Best for | Web apps with a backend | APIs, mobile, microservices |
| Overhead | DB lookup per request | Cryptographic verify per request |

**Rule of thumb:** If you control the frontend and backend together (a web app), use sessions. If you're building an API that third parties or mobile apps consume, use JWT.

The reason sessions beat JWT for web apps: you can log someone out immediately. With JWT you can't revoke a token — you have to wait for it to expire or build a denylist (which defeats the statelessness point).

---

## JWT Traps

- **Don't store in localStorage** — vulnerable to XSS. Any script on your page can read it. Use `httpOnly` cookies.
- **The "none" algorithm attack** — some old libraries accept `alg: none` (no signature). Always explicitly specify and enforce the algorithm.
- **Not validating `exp`** — tokens expire. Check it. Libraries usually do this but verify.
- **Signing with a weak secret** — use at least 256 bits of random entropy for HMAC, or use RS256 with a proper keypair.
- **Putting sensitive data in the payload** — JWT payload is base64-encoded, not encrypted. Anyone can decode it. Don't put PII or permissions you don't want exposed.

---

## Password Hashing — Only These Two

- **bcrypt** — battle-tested, widely supported, good default
- **argon2id** — modern, memory-hard, preferred for new systems

Never: MD5, SHA-1, SHA-256 raw, or any fast hash. Fast hashes are fast to brute force.

Work factor: bcrypt cost 10–12 is standard. Tune so hashing takes ~100–300ms on your hardware.

---

## OAuth — Implicit Flow Is Dead

The implicit flow (token returned directly in URL fragment) is deprecated. Use **Authorization Code + PKCE** for all OAuth flows including SPAs and mobile.

PKCE (Proof Key for Code Exchange) prevents authorization code interception attacks. All major providers support it.

---

## Common Oversights

- **Rate limit login endpoints** — without this, credential stuffing is trivial. 5 attempts per IP per minute is a reasonable starting point.
- **Account enumeration** — "user not found" vs "wrong password" tells attackers which emails are registered. Return the same generic message for both.
- **Timing attacks on login** — always hash the password even when the user doesn't exist (use a dummy hash) so response time doesn't leak whether the account exists.
- **Password reset tokens** — must be single-use, short-lived (15–60 min), and stored hashed in the DB. A reset link that works more than once is a vulnerability.
- **Session fixation** — always regenerate the session ID on login, not just on creation.
- **Logout** — actually invalidate the session server-side. Just clearing the cookie is not enough.
- **Remember me** — implement as a separate long-lived token stored in the DB, not by extending the session TTL.

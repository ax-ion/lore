# Secrets Management

---

## The Cardinal Rule

Secrets never touch the codebase. Not in config files. Not in comments. Not in test fixtures. Not in `.env.example` with real values. Not even for a second in git history — once it's committed, assume it's compromised and rotate it.

---

## Where Secrets Live

| Environment | Where |
|-------------|-------|
| Local dev | `.env` file, never committed |
| CI/CD | Platform secret store (GitHub Actions secrets, etc.) |
| Production | Environment variables injected at runtime, or a secrets manager |
| Shared team | 1Password / Bitwarden secrets manager — not Slack, not Notion |

---

## .env Files

- Always in `.gitignore` before the first commit
- `.env.example` with placeholder values is fine and encouraged — documents what's needed without leaking values
- Never log environment variables, even in debug mode — secrets live in env vars

---

## Rotation

Every secret should have an answer to: "how do I rotate this in under 10 minutes if it leaks?"

If you can't answer that, you haven't set it up right. For most services this means:
1. Generate new secret
2. Update secret store / env var
3. Redeploy or reload config
4. Revoke old secret

Secrets that can't be rotated without downtime are a design problem.

---

## What Gets Overlooked

- **Git history** — if a secret was ever committed, rotating it isn't enough. Remove it from history with `git filter-repo` or BFG Repo Cleaner, then force push, then rotate.
- **Log scrubbing** — structured logging pipelines can accidentally include request headers, env dumps, or error details that contain secrets. Audit what you're shipping to your log aggregator.
- **Container images** — secrets baked into Docker layers persist even if you add a later layer that deletes them. Use build args only for non-sensitive values; inject secrets at runtime.
- **Third-party services** — when you connect a service (Vercel, Render, Heroku) it often asks for env vars. Those values sit in that platform. Understand their security model.
- **Leaked via error messages** — stack traces, 500 pages, and debug modes can expose connection strings, API keys, and internal paths. Never expose raw errors to clients in production.
- **Short-lived credentials where possible** — IAM roles, OIDC tokens, and short-lived API tokens are better than long-lived static secrets. Rotate automatically instead of manually.

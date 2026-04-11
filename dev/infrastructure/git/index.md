# Git — Conventions & Workflow

---

## Commit Messages — The Format That Holds Up

```
<type>(<scope>): <short summary>

<body — optional, explains why not what>
```

Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`

Examples:
```
feat(auth): add refresh token rotation
fix(api): correct 500 on empty request body
refactor(db): extract connection pool into module
```

The summary line should complete the sentence: "If applied, this commit will ___."

**Why matters more than what.** The diff shows what changed. The message should explain why — what problem it solves, what decision was made, what trade-off was accepted.

---

## Branch Naming

```
feat/short-description
fix/short-description
chore/short-description
```

Keep it lowercase, hyphens not underscores, short enough to read at a glance.

---

## Branch Strategy — Keep It Simple

For small teams and solo projects: **trunk-based development**.
- `main` is always deployable
- Feature branches are short-lived (hours to days, not weeks)
- Merge via PR, delete branch after merge

Git Flow (develop/release/hotfix branches) is overkill for most projects. It adds process without adding protection.

---

## When to Squash vs Merge vs Rebase

| Strategy | When |
|----------|------|
| **Squash merge** | Feature branch with messy WIP commits — one clean commit on main |
| **Regular merge** | Branch with meaningful commit history worth preserving |
| **Rebase** | Keeping a branch current with main before merging — cleaner than merge commits |

Consistency matters more than which you pick. Pick one and document it.

---

## Branch Protection — Sensible Defaults

For any shared repo:
- Require PRs to merge to `main`
- Require at least 1 review for external contributors
- Don't enforce on admins for solo/small projects (you'll block yourself)
- Disable force push to `main`
- Disable branch deletion of `main`

---

## .gitignore Foundations

Always ignore before first commit. Things that always belong in `.gitignore`:
```
.env
.env.local
*.env
node_modules/
__pycache__/
*.pyc
.DS_Store
dist/
build/
*.log
```

Use [gitignore.io](https://gitignore.io) to generate language/framework-specific entries.

---

## What Gets Overlooked

- **`git blame` is not accusation, it's archaeology** — tells you when a line was written and links to the commit explaining why. Use it before changing anything unfamiliar.
- **Tags for releases** — `git tag v1.0.0 && git push origin v1.0.0`. Semantic versioning. Tags are how you mark deployable points in history.
- **`git stash` has a stack** — `git stash list` shows everything stashed. `git stash pop` gets the latest. Don't forget stashes exist.
- **Shallow clones for CI** — `git clone --depth 1` is much faster for CI pipelines that just need to build the latest commit.
- **Signing commits** — GPG or SSH signing proves a commit came from you. GitHub shows "Verified" badge. Worth setting up for any public project.

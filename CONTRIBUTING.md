# Contributing to lore

---

## What Belongs Here

Working knowledge. The kind of thing a senior practitioner knows that a junior doesn't — not because it's secret, but because it takes time and mistakes to internalize.

A good lore entry:
- Explains *why* a pattern works, not just *what* it is
- Covers the traps and overlooked details
- Is written for someone who already knows the basics
- Doesn't explain what a database is — explains what gets overlooked when designing schemas

A bad lore entry:
- Is a tutorial or getting-started guide
- Is a glossary of terms
- Reads like documentation or a Wikipedia article
- Covers things that are obvious to anyone who's done the work

---

## Format

Each entry is a single `index.md` in its topic directory. Structure:

```markdown
# Topic Name

One-line framing sentence — what this covers and why it matters.

---

## Section

Content. Focused. Practical.

---

## What Gets Overlooked

The non-obvious stuff. This section is the most important part of any entry.
```

---

## AI-Assisted Contributions

All changes go through a Pull Request. AI-generated entries must be declared in the PR and reviewed by a human maintainer. The standard is the same regardless of who wrote it — working knowledge, not filler.

---

## Adding a New Entry

1. Find the right directory or propose a new one in your PR description
2. Create `index.md` following the format above
3. Remove the stub line if replacing a placeholder
4. Open a PR

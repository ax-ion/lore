# Prompting

Not tricks. Structural patterns that produce consistent, reliable output from LLMs.

---

## System Prompt Is Identity, Not a To-Do List

A system prompt that reads like a list of rules produces rule-following behavior — brittle, literal, misses edge cases.

A system prompt that establishes identity, values, and context produces judgment — the model handles cases you didn't anticipate correctly because it understands *why*, not just *what*.

Bad:
```
You are a helpful assistant. Always be polite. Never discuss competitors.
Do not use bullet points. Answer in under 100 words.
```

Better:
```
You are a senior product advisor for a B2B SaaS company. Your role is to
help founders make confident product decisions. You speak directly, skip
pleasantries, and focus on tradeoffs and outcomes. You don't hedge when
you have a clear view.
```

---

## Role Before Task

Tell the model what it is before you tell it what to do. Role context shapes how it interprets everything that follows.

```
You are an expert in database schema design with 15 years of production experience.

Review the following schema and identify any indexing problems that would cause
performance issues at 10M rows.
```

---

## Few-Shot Beats Zero-Shot for Consistent Format

If you need structured output (JSON, a specific markdown format, a template), show examples. Don't describe the format — demonstrate it.

```
Extract the action items from this meeting transcript.

Format:
- [ ] Action item — @owner — due date

Example:
Input: "John said he'd update the docs by Friday and Sarah needs to review the PR."
Output:
- [ ] Update docs — @john — Friday
- [ ] Review PR — @sarah — no date

Now extract from: [transcript]
```

---

## Chain of Thought for Reasoning Tasks

For tasks that require multi-step reasoning, tell the model to think before answering.

```
Think through this step by step before giving your answer.
```

Or show the reasoning structure:
```
First, identify the constraints. Then, list the options that satisfy them.
Finally, recommend the best option and explain why.
```

This matters more for hard problems. For simple retrieval or formatting tasks, it adds noise.

---

## Temperature

- **0.0** — deterministic, best for code, structured output, factual extraction
- **0.3–0.5** — slightly varied, good for Q&A and analysis
- **0.7–1.0** — creative, brainstorming, writing
- **Above 1.0** — unpredictable, rarely useful

Default to 0 for anything a machine will parse. Use higher values when variance is a feature.

---

## Context Window Management

The model's attention isn't uniform across a long context. It pays most attention to:
1. The beginning (system prompt, framing)
2. The end (the most recent message)

Middle sections of long contexts get less reliable attention.

**Implication:** Put the most important constraints in the system prompt, not buried in the middle of a long user message. Put specific instructions close to the actual task.

---

## What Gets Overlooked

- **Negative instructions fail** — "don't include caveats" often doesn't work. "Be direct. State your conclusion first." works better. Tell it what to do, not what not to do.
- **Asking for confidence is useful** — "how confident are you in this?" after a complex answer often surfaces important uncertainty the model didn't volunteer.
- **Model behavior drifts across a long conversation** — instructions given in message 1 lose influence by message 30. Re-anchor in system prompt or repeat key constraints periodically.
- **JSON mode / structured output** — if your provider offers it, use it. Don't try to regex-parse JSON out of freeform text when you can get a guaranteed valid JSON response.
- **Prompt caching** — for long system prompts or large context blocks that repeat across calls, use prompt caching (Anthropic, OpenAI both support it). Can reduce costs 80-90% on repeated prefixes.

# SQL — Schema Design & Patterns

---

## Schema Design Principles

**Design for queries, not for normalization.**
Normalization is a tool, not a goal. A perfectly normalized schema that requires 8 joins to display a user's dashboard is worse than a slightly denormalized one that's fast and readable.

Ask: "What queries will this schema serve?" Design the schema to make those queries simple.

---

## Naming Conventions — Pick One, Never Mix

| Thing | Convention |
|-------|-----------|
| Tables | `snake_case`, plural (`users`, `order_items`) |
| Columns | `snake_case` (`created_at`, `user_id`) |
| Primary keys | `id` (simple) or `{table}_id` for clarity in joins |
| Foreign keys | `{referenced_table_singular}_id` (`user_id`, `order_id`) |
| Booleans | `is_` or `has_` prefix (`is_active`, `has_verified_email`) |
| Timestamps | `created_at`, `updated_at`, `deleted_at` |

---

## Always Include

```sql
id          BIGSERIAL PRIMARY KEY,  -- or UUID
created_at  TIMESTAMPTZ NOT NULL DEFAULT NOW(),
updated_at  TIMESTAMPTZ NOT NULL DEFAULT NOW()
```

`TIMESTAMPTZ` (timestamp with timezone) not `TIMESTAMP`. Store in UTC, display in local time in the application layer.

---

## Soft Deletes

Add `deleted_at TIMESTAMPTZ NULL`. When "deleted," set it to `NOW()` instead of removing the row.

Benefits: audit trail, accidental delete recovery, foreign key integrity.

Cost: every query needs `WHERE deleted_at IS NULL`. Easy to forget, easy to leak deleted records.

Use a view or a default filter in your ORM to handle this automatically.

---

## Indexing — What Actually Matters

**Index:**
- Every foreign key
- Columns in `WHERE` clauses that filter large tables
- Columns in `ORDER BY` when combined with `LIMIT`
- Columns in `JOIN` conditions

**Don't blindly index everything** — indexes slow down writes and consume storage. An unused index is a net negative.

Check what's missing: `pg_stat_user_indexes` (Postgres) shows index usage stats.

---

## Migrations

- One change per migration — small, reversible, reviewable
- Never edit a migration that's been run in production — add a new one
- Test migrations on production-sized data before running in production — what takes 1ms on dev can lock a 50M row table for 20 minutes in prod
- For large tables: add columns as nullable first, backfill, then add constraints
- Postgres-specific: adding a column with a non-null default rewrites the whole table in older versions. Use `ADD COLUMN ... DEFAULT` + `ALTER COLUMN ... SET NOT NULL` separately.

---

## Transactions — Use Them

Any operation that modifies more than one table should be in a transaction. If step 2 fails, step 1 rolls back.

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

Don't hold transactions open longer than needed — they hold locks.

---

## What Gets Overlooked

- **N+1 queries** — loading a list of records then querying each one individually in a loop. Fix with JOINs or eager loading in your ORM. A page that makes 200 queries to render is a bug.
- **EXPLAIN ANALYZE** — run it on any slow query before guessing. It shows exactly what the planner does and where time is spent.
- **Connection pooling** — databases have connection limits. Always use a connection pool (PgBouncer, built-in ORM pool). Opening a new connection per request kills performance.
- **TEXT vs VARCHAR** — in Postgres, TEXT and VARCHAR are identical in performance. Don't add VARCHAR length constraints unless the constraint is a real business rule.
- **JSONB for flexible data** — Postgres JSONB is indexable, queryable, and useful for genuinely variable schemas. Don't reach for a NoSQL database just because you have some flexible fields.

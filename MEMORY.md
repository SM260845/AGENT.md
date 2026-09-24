# MEMORY.md — The Logbook 📓

> Durable facts and lessons from past sessions. Read **before repeating old
> mistakes**. This file is **append-only** (PROTOCOL.md, Article IV): never
> rewrite or delete past entries — append a superseding entry instead.

---

## Entry schema

Append entries to the **Log** section below, newest last, using exactly this
format (see the `update-memory-log` skill for step-by-step instructions):

```markdown
### YYYY-MM-DD — <short title>
- **Task:** what was being done
- **Lesson:** the durable fact or lesson learned
- **Citation:** file:line, PR/commit reference, or `User input: "<quote>"`
```

Rules:

- One entry per durable lesson; skip temporary or task-specific details.
- To correct an earlier entry, append a new entry whose Lesson starts with
  `Supersedes <date> — <title>:`.
- Never store secrets, credentials, or personal data.

---

## Log

### 2026-09-24 — Repository skeleton completed
- **Task:** Implement the balanced innovation roadmap (Tiers 1–3).
- **Lesson:** All 12 checklist files now exist; `scripts/preflight-check`
  audits them and CI enforces the AGENTS.md/README.md mirror on every push.
- **Citation:** PROTOCOL.md:1, scripts/preflight-check:1,
  .github/workflows/preflight.yml:1

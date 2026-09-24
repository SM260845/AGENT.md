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

### 2026-09-24 — Skills toolbox scaffolded (retroactive log)
- **Task:** Create `SKILLS.md` and the starter skills `mirror-docs`,
  `add-skill`, and `checklist-audit` under `.github/skills/` (PR #3); the
  session ended without logging to `MEMORY.md`, so this entry is appended
  retroactively to finalize it.
- **Lesson:** Skills follow the open Agent Skills standard (`SKILL.md` with
  `name`/`description` frontmatter) auto-discovered from `.github/skills/`,
  and every skill must have a row in the "Installed skills" table in
  `SKILLS.md`. Every session must end by logging its durable lesson here —
  the LOG step of the loop is not optional.
- **Citation:** PR #3 (SM260845/AGENT.md), SKILLS.md:42-51, PROTOCOL.md:46-50

### 2026-09-24 — Last two sessions verified and finalized
- **Task:** Finalize the sessions behind PR #3 (skills toolbox) and PR #4
  (checklist skeleton): verify their merged state and complete their missing
  loop steps.
- **Lesson:** Both PRs' content is merged into `main` (commits c35ac64 and
  034bbb3); `scripts/preflight-check` passes — mirror intact, all 12
  checklist files present, all 6 skills registered. Finalizing a session
  means running the VERIFY step (`scripts/preflight-check` must pass,
  PROTOCOL.md Article III.4) and the LOG step (append the lesson here).
- **Citation:** PROTOCOL.md:32, AGENTS.md:88-101, commits c35ac64 & 034bbb3

### 2026-09-24 — Guided simulation and first external skill imports
- **Task:** Run a guided simulation of the agent loop and experiment with
  skills from the Claude catalog (anthropics/skills); report the results in
  `docs/reports/2026-09-24-guided-simulation.md`.
- **Lesson:** Claude-format skills import unmodified and pass
  `scripts/preflight-check` (folded-scalar descriptions and extra frontmatter
  keys included), but licensing in anthropics/skills varies per skill: only
  import skills shipping their own Apache-2.0 `LICENSE.txt` (keep it), skip
  unlicensed ones (e.g. `doc-coauthoring`) and the source-available document
  skills. `internal-comms` and `discernment-nudge` are now installed.
- **Citation:** docs/reports/2026-09-24-guided-simulation.md:1,
  SKILLS.md:52-53, .github/skills/internal-comms/LICENSE.txt:1

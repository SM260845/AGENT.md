# UTILITIES.md — The Utility Belt 🛠️

> Helper scripts, one-liners, and shared tooling. Read **before hand-rolling
> something a utility already does**.

---

## Scripts (`scripts/`)

| Utility | Command | What it does |
|---------|---------|--------------|
| Preflight check | `scripts/preflight-check` | Audits the repository against the flight checklist: verifies the AGENTS.md/README.md mirror, reports which checklist files exist or are missing, and validates skill frontmatter. Exits non-zero on failure. Also runs in CI. |

## One-liners

| Task | Command |
|------|---------|
| Verify the mirror manually | `diff AGENTS.md README.md && echo OK` |
| Re-sync README from AGENTS | `cp AGENTS.md README.md` (or the reverse — see the `sync-mirrored-files` skill) |
| List installed skills | `ls .github/skills/` |

## Adding a utility

1. Put executable scripts in `scripts/`, POSIX-shell compatible where
   possible, with a usage comment at the top.
2. Register the utility in the table above.
3. Keep utilities dependency-free; per the roadmap, no custom tooling beyond
   markdown, one CI workflow, and simple scripts until usage justifies it.

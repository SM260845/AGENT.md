# WORKFLOWS.md — The Assembly Line 🏭

> Optimised, repeatable task pipelines and automation. Read **before running
> or designing a multi-step process**.

---

## Automated workflows (`.github/workflows/`)

| Workflow | File | What it does |
|----------|------|--------------|
| Preflight | `.github/workflows/preflight.yml` | Runs `scripts/preflight-check` on every push and pull request: fails if the AGENTS.md/README.md mirror is broken, a checklist file is missing, or a skill has invalid frontmatter |

## Agent pipelines

### Change pipeline (any edit to this repository)

1. Ingest the priority files (`AGENTS.md` checklist, in order).
2. Plan using `SKILLS.md`; pick an installed skill if one matches.
3. Act within `PROTOCOL.md`; if editing `AGENTS.md` or `README.md`, follow
   the `sync-mirrored-files` skill.
4. Verify with `scripts/preflight-check`.
5. Log durable lessons via the `update-memory-log` skill.

### Bootstrap pipeline (new instance from this template)

1. Click **Use this template** on GitHub (this repository is intended to be
   configured as a template repository).
2. In the new repo, follow the `new-instance-bootstrap` skill to fill in the
   `WIKI.yaml` identity fields and set `role: spoke`.
3. Open a PR against the hub adding the new instance to `CATALOG.md`.

## Designing a new pipeline

Document it here as a numbered list, reuse installed skills as steps, and
keep it short enough to execute without re-reading twice.

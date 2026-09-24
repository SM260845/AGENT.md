# SKILLS.md — The Toolbox 🧰

> Reusable skills, playbooks, and how to invoke them. Read this **before
> choosing an approach** to any task: if a skill already covers the work,
> use the skill instead of improvising.

---

## How skills work

Skills follow the open Agent Skills standard: each skill is a directory
containing a `SKILL.md` file with YAML frontmatter (`name`, `description`)
followed by Markdown instructions. Copilot and Claude auto-load skills from:

- `.github/skills/` ← canonical location in this repository
- `.claude/skills/` (compatible, not used here)
- `.agents/skills/` (compatible, not used here)

Claude-format skills work unmodified.

## Invoking a skill

1. Match the task against the `description` of each installed skill.
2. Open `.github/skills/<name>/SKILL.md` and follow its steps exactly.
3. If steps conflict with `PROTOCOL.md`, the protocol wins — stop and ask.

## Installed skills

| Skill | Location | Purpose |
|-------|----------|---------|
| `sync-mirrored-files` | `.github/skills/sync-mirrored-files/SKILL.md` | Keep `AGENTS.md` and `README.md` byte-for-byte identical |
| `update-memory-log` | `.github/skills/update-memory-log/SKILL.md` | Append a correctly formatted entry to `MEMORY.md` |
| `new-instance-bootstrap` | `.github/skills/new-instance-bootstrap/SKILL.md` | Configure a fresh instance created from this template |

## Adding a new skill

1. Create `.github/skills/<kebab-case-name>/SKILL.md` with `name` and
   `description` frontmatter.
2. Register it in the "Installed skills" table above.
3. Run `scripts/preflight-check` — it validates skill frontmatter.
4. Log the addition in `MEMORY.md`.

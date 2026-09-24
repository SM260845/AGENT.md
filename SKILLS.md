# SKILLS.md — The Toolbox 🧰

> Reusable skills, playbooks, and how to invoke them. Read this **before
> choosing an approach** to any task: if a skill already covers the work,
> use the skill instead of improvising. This file is the human-readable index
> of the skills available to agents working in this repository.

---

## How skills work

Skills follow the open **Agent Skills** standard: each skill is a directory
containing a `SKILL.md` file with YAML frontmatter (`name`, `description`)
followed by Markdown instructions. Copilot and Claude auto-load skills from:

- `.github/skills/` ← canonical location in this repository
- `.claude/skills/` (compatible, not used here)
- `.agents/skills/` (compatible, not used here)

Claude-format skills work unmodified.

At runtime the agent scans each skill's `description` and loads the full skill
only when it matches the task. You can also invoke a skill explicitly by
naming it in your prompt.

### Where agents discover skills

| Path | Scope |
|------|-------|
| `.github/skills/<name>/SKILL.md` | This repository (canonical Copilot path — used here) |
| `.claude/skills/`, `.agents/skills/` | Repository (also read by Copilot; Claude-native / vendor-neutral) |
| `~/.copilot/skills/`, `~/.agents/skills/` | Personal, across all repositories |

Reference: [Custom skills — GitHub Docs](https://docs.github.com/copilot/how-tos/copilot-sdk/use-copilot-sdk/custom-skills)

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
| `mirror-docs` | `.github/skills/mirror-docs/SKILL.md` | Keep `AGENTS.md` and `README.md` byte-for-byte identical during edits and review |
| `add-skill` | `.github/skills/add-skill/SKILL.md` | Create a new skill or install one from an external skill catalog |
| `checklist-audit` | `.github/skills/checklist-audit/SKILL.md` | Audit which flight-checklist files and support directories exist |

## Where to find more skills

Curated catalogs of ready-to-use `SKILL.md` skills, all compatible with this
repository's format:

| Catalog | Notes |
|---------|-------|
| [anthropics/skills](https://github.com/anthropics/skills) | Anthropic's official Agent Skills repo — the reference source |
| [github/awesome-copilot](https://github.com/github/awesome-copilot) | GitHub's community collection of Copilot instructions, agents, and skills |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | Large curated collection of community and official skills |
| [wshobson/agents](https://github.com/wshobson/agents) | Multi-harness skill/agent marketplace with explicit Copilot support |
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | Broad catalog of Claude-compatible skills that also work here |
| [seb1n/awesome-ai-agent-skills](https://github.com/seb1n/awesome-ai-agent-skills) | Ready-to-use `SKILL.md` workflows across many domains |

## Adding a new skill

1. Create `.github/skills/<kebab-case-name>/SKILL.md` with `name` and
   `description` frontmatter.
2. Register it in the "Installed skills" table above.
3. If importing from an external catalog, verify the license permits reuse and
   keep any required attribution or LICENSE files.
4. Run `scripts/preflight-check` — it validates skill frontmatter.
5. Log the addition in `MEMORY.md`.

## Rules of the toolbox

1. **Every skill is registered here.** A skill folder without a row in the
   "Installed skills" table is unfinished work.
2. **Descriptions are the API.** Agents select skills by the frontmatter
   `description` — keep it accurate and include the trigger ("Use when…").
3. **Folder name = frontmatter `name`.** Lowercase, hyphenated, matching.

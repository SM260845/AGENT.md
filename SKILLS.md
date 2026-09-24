# SKILLS.md — The Toolbox 🧰

> Checklist item **4** of `AGENTS.md`. This file is the human-readable index of
> the skills available to agents working in this repository. The skills
> themselves live under [`.github/skills/`](.github/skills/).

---

## How skills work

Skills follow the open **Agent Skills** standard shared by GitHub Copilot,
Claude Code, and other compatible agents: one folder per skill containing a
`SKILL.md` with YAML frontmatter (`name` + `description`) followed by Markdown
instructions. Claude `SKILL.md` files work in Copilot unmodified.

At runtime the agent scans every skill's `description` and loads the full skill
(plus any bundled scripts or reference files) **only when it matches the
task** — read, select, load. You can also invoke a skill explicitly by naming
it in your prompt.

### Where agents discover skills

| Path | Scope |
|------|-------|
| `.github/skills/<name>/SKILL.md` | This repository (canonical Copilot path — used here) |
| `.claude/skills/`, `.agents/skills/` | Repository (also read by Copilot; Claude-native / vendor-neutral) |
| `~/.copilot/skills/`, `~/.agents/skills/` | Personal, across all repositories |

Reference: [Custom skills — GitHub Docs](https://docs.github.com/copilot/how-tos/copilot-sdk/use-copilot-sdk/custom-skills)

---

## Installed skills

| Skill | What it does | When to invoke it |
|-------|--------------|-------------------|
| [`mirror-docs`](.github/skills/mirror-docs/SKILL.md) | Keeps `AGENTS.md` and `README.md` byte-for-byte identical | Whenever either file is edited or reviewed |
| [`add-skill`](.github/skills/add-skill/SKILL.md) | Creates a new skill or installs one from an external catalog | When adding, writing, or importing a skill |
| [`checklist-audit`](.github/skills/checklist-audit/SKILL.md) | Reports which flight-checklist files exist or are missing | At task start, or when checking repo health |

---

## Where to find more skills

Curated catalogs of ready-to-use `SKILL.md` skills, all compatible with this
repository's format:

| Catalog | Notes |
|---------|-------|
| [anthropics/skills](https://github.com/anthropics/skills) | Anthropic's official Agent Skills repo — the reference source (document skills, skill-creator, and more) |
| [github/awesome-copilot](https://github.com/github/awesome-copilot) | GitHub's community collection of Copilot instructions, agents, and skills |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 1000+ curated skills from official teams and the community |
| [wshobson/agents](https://github.com/wshobson/agents) | Multi-harness skill/agent marketplace with explicit Copilot support |
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | 380+ skills across engineering, product, marketing, and ops |
| [seb1n/awesome-ai-agent-skills](https://github.com/seb1n/awesome-ai-agent-skills) | 100+ complete ready-to-use SKILL.md workflows |

To install one, follow the [`add-skill`](.github/skills/add-skill/SKILL.md)
skill: check the license, copy the skill folder into `.github/skills/`, and
register it in the table above.

---

## Rules of the toolbox

1. **Every skill is registered here.** A skill folder without a row in the
   "Installed skills" table is unfinished work.
2. **Descriptions are the API.** Agents select skills by the frontmatter
   `description` — keep it accurate and include the trigger ("Use when…").
3. **Folder name = frontmatter `name`.** Lowercase, hyphenated, matching.
4. **Respect licenses.** Imported skills keep their LICENSE files and a source
   link in the table above.

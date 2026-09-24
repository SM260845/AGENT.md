---
name: add-skill
description: Create a new agent skill or install one from an external skill catalog into .github/skills/. Use when asked to add, write, import, or update a skill in this repository.
---

# Add Skill

Skills follow the open Agent Skills standard: one folder per skill under
`.github/skills/`, containing a `SKILL.md` with YAML frontmatter. Claude
`SKILL.md` files work unmodified.

## Skill format

```
.github/skills/<skill-name>/
└── SKILL.md          # required
└── (optional scripts, references, assets)
```

`SKILL.md` must begin with frontmatter:

```yaml
---
name: skill-name        # lowercase, hyphens, must match the folder name
description: What it does and when to use it (agents select skills by this)
---
```

Followed by Markdown instructions. Keep the description one or two sentences —
it is the only part scanned during skill selection, so it must state both the
capability and the trigger ("Use when…").

## Writing a new skill

1. Pick a short, hyphenated name; create `.github/skills/<name>/SKILL.md`.
2. Write frontmatter, then step-by-step instructions. Include exact commands
   where possible; agents follow commands more reliably than prose.
3. Keep it under ~500 lines. Move bulky reference material into sibling files
   and link to them from `SKILL.md`.
4. Register the skill in the table in `SKILLS.md`.

## Installing from an external catalog

1. Browse a catalog (see "Where to find skills" in `SKILLS.md`), e.g.
   `anthropics/skills`, `github/awesome-copilot`,
   `VoltAgent/awesome-agent-skills`.
2. Check the skill's license permits reuse; keep its LICENSE file if it has one.
3. Copy the whole skill folder into `.github/skills/<name>/`.
4. Register it in `SKILLS.md` with a link to its source.

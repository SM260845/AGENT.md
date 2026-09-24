---
name: checklist-audit
description: Audit which flight-checklist files from AGENTS.md exist in the current repository and report what is missing. Use at the start of a task or when asked to check repository configuration health.
---

# Checklist Audit

`AGENTS.md` defines a flight checklist of priority and specialty files. This
skill verifies which exist so the agent (or a human) knows what support is
available and what is still missing.

## Instructions

1. Run the audit:

   ```bash
   for f in AGENTS.md README.md PROTOCOL.md SKILLS.md WIKI.yaml CATALOG.md \
            MEMORY.md PLUGINS.md KNOWLEDGE.md WORKFLOWS.md SUPPORT.md UTILITIES.md; do
     [ -e "$f" ] && echo "PRESENT  $f" || echo "MISSING  $f"
   done
   for d in .github/skills .github/plugins .github/workflows docs scripts; do
     [ -d "$d" ] && echo "PRESENT  $d/" || echo "MISSING  $d/"
   done
   ```

2. Report the results grouped as **priority** (items 1–7 of the checklist) and
   **specialty** (items 8–12).
3. Per `AGENTS.md`: a missing file is not an error — say so and proceed with
   the files that do exist. Do not create missing files unless asked.
4. If `AGENTS.md` and `README.md` differ, flag it and apply the `mirror-docs`
   skill.

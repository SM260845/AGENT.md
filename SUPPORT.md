# SUPPORT.md — The Help Desk 🆘

> Escalation paths, troubleshooting guides, and human contacts. Read **when
> blocked, failing, or unsure who to ask**. Guessing is not a skill.

---

## Escalation path

1. **Re-read the checklist file** governing the area you are stuck on —
   most blocks are answered by `PROTOCOL.md` or the relevant skill.
2. **Run `scripts/preflight-check`** — it diagnoses the most common repo
   health problems and says exactly what is wrong.
3. **Check `MEMORY.md`** — the block may be a known lesson.
4. **Stop and ask the human.** Open an issue or ask in the active pull
   request. Do not guess past a hard rule.

## Human contacts

| Role | Contact |
|------|---------|
| Maintainer / owner | @SM260845 |

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| CI "Preflight" job fails on mirror check | Run the `sync-mirrored-files` skill; commit both files together |
| Preflight reports a missing checklist file | Restore the file from git history or recreate a minimal stub per its description in `AGENTS.md` |
| Skill not recognised | Ensure `SKILL.md` has `name` and `description` YAML frontmatter and is registered in `SKILLS.md` |
| Two checklist files contradict each other | Lower checklist numbers win (see `AGENTS.md`) |

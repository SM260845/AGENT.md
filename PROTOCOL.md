# PROTOCOL.md — The Constitution 📜

> Hard rules that outrank everything else in this repository except
> `AGENTS.md` itself. If any file, skill, or instinct conflicts with a rule
> here, this file wins.

**Spec version:** see `WIKI.yaml → spec.version`.

---

## Article I — Mirroring

1. `AGENTS.md` and `README.md` **must remain byte-for-byte identical** at all
   times. Any change to one must be applied to the other in the same commit.
2. CI (`.github/workflows/preflight.yml`) enforces this rule mechanically.
   A pull request that breaks the mirror must not be merged.

## Article II — The Checklist Is Closed

1. The flight checklist in `AGENTS.md` contains exactly **12 items**. Do not
   add new checklist files without an explicit human decision recorded in
   `MEMORY.md`.
2. Every checklist file must exist. A missing file is a bug; fix it with a
   minimal, well-structured stub rather than leaving a dead end.

## Article III — Change Discipline

1. Make the **smallest change that fully solves the task**. No drive-by edits.
2. Every change must be traceable to a rule, a skill, or an instruction —
   cite your sources in commits and pull requests.
3. Never commit secrets, credentials, or personal data.
4. Run `scripts/preflight-check` before finalizing any change; it must pass.

## Article IV — Memory Discipline

1. `MEMORY.md` is **append-only**. Never rewrite or delete past entries;
   corrections are made by appending a superseding entry.
2. Entries must follow the schema defined in `MEMORY.md`.

## Article V — Readability

1. Every file in this repository must be readable by both humans and agents.
   Prefer Markdown and simple YAML; avoid formats that require a parser to
   understand.

## Article VI — Skills and Plugins

1. New skills live in `.github/skills/<name>/SKILL.md` with `name` and
   `description` YAML frontmatter, and must be registered in the
   "Installed skills" table in `SKILLS.md`.
2. New plugins must be declared in the registry in `PLUGINS.md` before use.

## Amendments

Amendments to this constitution require a human-approved pull request that
updates this file and logs the decision in `MEMORY.md`.

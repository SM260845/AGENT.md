# KNOWLEDGE.md — The Library 📚

> Domain knowledge, references, and deep context. Read **when a task needs
> subject-matter depth beyond the briefing** in `README.md`.

---

## Core concepts

- **Flight checklist** — the ordered reading list in `AGENTS.md` that every
  agent ingests before acting. Priority files form the core loop; specialty
  files are extensions loaded on demand.
- **Hub and spokes** — this repository (hub) defines the spec; other
  repositories (spokes) follow it and are mapped in `CATALOG.md`.
- **Spec version** — the semver in `WIKI.yaml → spec.version` identifying
  which AGENTS.md protocol format an instance follows.

## External references

- Agent Skills standard (Copilot custom skills):
  https://docs.github.com/copilot/how-tos/copilot-sdk/use-copilot-sdk/custom-skills
- AGENTS.md convention: https://agents.md

## Extending the library

Add durable domain knowledge here or under `docs/`. Keep session-specific
lessons in `MEMORY.md` instead; this file is for reference material, not a
logbook.

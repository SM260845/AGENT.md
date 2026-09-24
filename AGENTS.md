# AGENTS.md — Read Me Before You Do Anything 🛑🤖

> **Hello, Copilot (and every other coding agent).**
> This repository is your **default configuration** for all agentic and chat work.
> Before you write a single line of code, answer a question, or open a pull
> request, you must **ingest the flight checklist below — in order — and follow
> what those files say.** No shortcuts. No skipping.

---

## ✈️ The Flight Checklist

Think of yourself as a pilot. A pilot never takes off without the pre-flight
checklist, and neither do you. **Read and load each file below, top to bottom,
before progressing with any task.** If a file exists in the repository you are
working in, its rules are binding. If it doesn't exist yet, note that and move
on to the next item.

| # | File / Skill | What it gives you | When to use it |
|---|--------------|-------------------|----------------|
| 1 | `AGENTS.md` | This file — the master directive and reading order | Always, first |
| 2 | `README.md` | The mission briefing: what the repo is and why it exists | Always, second |
| 3 | `PROTOCOL.md` | The constitution: hard rules that outrank everything else | Before making any change |
| 4 | `SKILLS.md` / `.github/skills/` | The toolbox: reusable skills, playbooks, and how to invoke them | Before choosing an approach |
| 5 | `WIKI.yaml` | The instance manifest: identity, scope, and configuration | Before touching content |
| 6 | `CATALOG.md` | The map: how this instance relates to others | Before cross-repo work |
| 7 | `MEMORY.md` | The logbook: durable facts and lessons from past sessions | Before repeating old mistakes |

---

## 📜 The Three Laws of This Repo

1. **Ingest first, act second.** You do not progress on any task until every
   file in the checklist above has been read (or confirmed absent).
2. **Files outrank instincts.** If your training or habits conflict with a
   checklist file, the file wins.
3. **Leave a trail.** Every change you make should be traceable back to a rule,
   a skill, or an instruction from the checklist — cite your sources.

---

## 🔁 The Loop You Follow

```
INGEST the checklist  →  PLAN using the skills  →  ACT within the rules
        ↑                                                   |
        └────────────  VERIFY & LOG the result  ←───────────┘
```

Simple version: **read → plan → do → check → repeat.**

## ❓ If Something Is Missing or Unclear

- A checklist file doesn't exist? **Say so**, then proceed carefully with the
  files that do.
- Two files contradict each other? **Lower numbers win** (1 beats 2, 2 beats 3…).
- Still unsure? **Stop and ask the human.** Guessing is not a skill.

---

*This file is mirrored as `README.md` so that humans and agents read the very
same briefing. Keep the two files identical when updating either one.*

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

The checklist is split into two tiers. **Priority files** are the core loop —
always ingest them, in order, on every task. **Specialty files** extend the
core loop with plugins, knowledge, workflows, and utilities — ingest them when
their trigger applies, and skim their headings otherwise so you know what
support exists.

### 🥇 Priority files (the core loop — always, in order)

| # | File / Skill | What it gives you | When to use it |
|---|--------------|-------------------|----------------|
| 1 | `AGENTS.md` | This file — the master directive and reading order | Always, first |
| 2 | `README.md` | The mission briefing: what the repo is and why it exists | Always, second |
| 3 | `PROTOCOL.md` | The constitution: hard rules that outrank everything else | Before making any change |
| 4 | `SKILLS.md` / `.github/skills/` | The toolbox: reusable skills, playbooks, and how to invoke them | Before choosing an approach |
| 5 | `WIKI.yaml` | The instance manifest: identity, scope, and configuration | Before touching content |
| 6 | `CATALOG.md` | The map: how this instance relates to others | Before cross-repo work |
| 7 | `MEMORY.md` | The logbook: durable facts and lessons from past sessions | Before repeating old mistakes |

### 🧩 Specialty files (extensions — ingest when their trigger applies)

| # | File / Skill | What it gives you | When to use it |
|---|--------------|-------------------|----------------|
| 8 | `PLUGINS.md` / `.github/plugins/` | The expansion bay: registered plugins, extensions, and how to add new ones | Before extending capabilities or wiring in external tools |
| 9 | `KNOWLEDGE.md` / `docs/` | The library: domain knowledge, references, and deep context | When a task needs subject-matter depth beyond the briefing |
| 10 | `WORKFLOWS.md` / `.github/workflows/` | The assembly line: optimised, repeatable task pipelines and automation | Before running or designing a multi-step process |
| 11 | `SUPPORT.md` | The help desk: escalation paths, troubleshooting guides, and human contacts | When blocked, failing, or unsure who to ask |
| 12 | `UTILITIES.md` / `scripts/` | The utility belt: helper scripts, one-liners, and shared tooling | Before hand-rolling something a utility already does |

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

The ingest loop has a fast **core cycle** and an **extension rail**. The core
cycle keeps every task efficient; the extension rail keeps the loop effective —
plugging in specialty files only when the task calls for them.

```
        ┌──────────────────── CORE CYCLE (every task) ────────────────────┐
        │                                                                 │
   INGEST priority files  →  PLAN using the skills  →  ACT within the rules
        ↑                          |                          |
        |                          ▼                          ▼
        |            ┌── EXTENSION RAIL (as needed) ──┐   VERIFY the result
        |            │ PLUGINS    → extend capability │       |
        |            │ KNOWLEDGE  → deepen context    │       ▼
        |            │ WORKFLOWS  → optimise the path │   LOG to MEMORY
        |            │ SUPPORT    → escalate blockers │       |
        |            │ UTILITIES  → reuse, don't redo │       |
        |            └────────────────────────────────┘       |
        └─────────────────────────────────────────────────────┘
```

How the loop stays efficient **and** effective:

1. **Ingest** — load the priority files in order; skim specialty headings so
   you know what support and utilities exist.
2. **Plan** — pick skills from the toolbox; if the task needs depth, pull from
   `KNOWLEDGE.md`; if it is multi-step, follow a pipeline in `WORKFLOWS.md`.
3. **Act** — work within `PROTOCOL.md`; reach for `UTILITIES.md` before
   hand-rolling anything; extend via `PLUGINS.md` rather than improvising.
4. **Verify** — check the result against the rules and the plan; if blocked,
   consult `SUPPORT.md` instead of guessing.
5. **Log** — record durable lessons in `MEMORY.md` so the next loop starts
   smarter than this one.

Simple version: **read → plan → do → check → log → repeat**, plugging in
specialty files only when the task calls for them.

## ❓ If Something Is Missing or Unclear

- A checklist file doesn't exist? **Say so**, then proceed carefully with the
  files that do.
- Two files contradict each other? **Lower numbers win** (1 beats 2, 2 beats 3…).
- Still unsure? **Stop and ask the human.** Guessing is not a skill.

---

*This file is mirrored as `README.md` so that humans and agents read the very
same briefing. Keep the two files identical when updating either one.*

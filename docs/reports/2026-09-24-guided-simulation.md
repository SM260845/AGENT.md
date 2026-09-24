# Guided Simulation & Reporting Exercise — 2026-09-24

> A dry run of the full agent loop defined in `AGENTS.md`, plus a
> compatibility experiment installing unmodified Claude-format skills from
> the [anthropics/skills](https://github.com/anthropics/skills) catalog.
> Filed under `docs/` per `KNOWLEDGE.md` ("Extending the library").

---

## 1. Exercise scope

- **Simulate** one complete pass of the loop: INGEST → PLAN → ACT → VERIFY → LOG.
- **Experiment** with external Claude-repo skills to test the claim in
  `SKILLS.md` that "Claude-format skills work unmodified."
- **Report** the results using the newly installed `internal-comms` skill's
  3P format (dogfooding).

## 2. Loop simulation trace

| Step | What was done | Outcome |
|------|---------------|---------|
| INGEST | Read all 7 priority files in order, skimmed all 5 specialty files | All 12 checklist files present; no contradictions found |
| PLAN | Matched task against `SKILLS.md`; selected `checklist-audit`, `add-skill`, and `update-memory-log` | Every step of the task was covered by an installed skill — no improvisation needed |
| ACT | Installed `internal-comms` and `discernment-nudge` from anthropics/skills (Apache-2.0, LICENSE.txt retained); registered both in `SKILLS.md` | 8 files added, 1 table updated; no edits to mirrored files |
| VERIFY | Ran `scripts/preflight-check` before and after | PASS both times; mirror intact, 8/8 skills valid and registered |
| LOG | Appended durable lesson to `MEMORY.md` via `update-memory-log` | Entry follows schema, append-only preserved |

## 3. Compatibility experiment findings

1. **Claude skills work unmodified — confirmed.** Both imported `SKILL.md`
   files passed `scripts/preflight-check` frontmatter validation as-is,
   including `discernment-nudge`'s YAML folded-scalar description
   (`description: >`) and `internal-comms`'s extra `license:` key.
2. **Licensing varies per skill in anthropics/skills.** Skills shipping a
   `LICENSE.txt` are Apache-2.0; the `docx`/`pdf`/`pptx`/`xlsx` document
   skills are source-available (not open source); some skills (e.g.
   `doc-coauthoring`) ship no license file at all and were therefore **not**
   imported. The `add-skill` step "check the license permits reuse" is a real
   gate, not a formality.
3. **Skill size varies by two orders of magnitude.** `internal-comms` is
   ~1.5 KB + 4 example files; `skill-creator` is ~33 KB with scripts, agents,
   and an eval viewer. Per `add-skill`'s ~500-line guidance, large multi-asset
   skills were deliberately skipped for this governance repo.
4. **The preflight validator is tolerant but shallow.** It accepts any
   non-empty `name`/`description` value, so a folded scalar passes even though
   the validator never reads the folded text. Acceptable today; worth noting
   if stricter description-based skill selection is ever automated.

## 4. Recommendations

- Prefer catalog skills that ship their own `LICENSE.txt`; record the license
  in the `SKILLS.md` table row (done for both imports).
- Keep imports scoped to skills relevant to this repo's governance mission
  (`WIKI.yaml → scope`); document-manipulation skills belong in spokes that
  need them.
- Consider a future preflight enhancement to flag skill folders lacking a
  registered source/license when imported (log a `MEMORY.md` decision first —
  PROTOCOL.md Article II keeps the checklist closed, but scripts may evolve).

## 5. 3P update (via the `internal-comms` skill)

🛫 AGENT.md Hub (Sep 18 – Sep 24, 2026)
Progress: Ran a full guided simulation of the agent loop; imported 2 Apache-2.0 skills from anthropics/skills unmodified, growing the toolbox from 6 to 8 skills with preflight passing 8/8.
Plans: Exercise `discernment-nudge` and `internal-comms` in upcoming sessions; evaluate one skill from github/awesome-copilot for the next import round.
Problems: Several catalog skills lack license files, blocking import; large multi-asset skills (e.g. skill-creator, 33 KB+) exceed the toolbox's ~500-line guidance.

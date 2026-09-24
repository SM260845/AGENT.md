---
name: mirror-docs
description: Keep AGENTS.md and README.md byte-for-byte identical. Use whenever editing, reviewing, or committing changes to either file in this repository.
---

# Mirror Docs

`AGENTS.md` and `README.md` are the same briefing for agents and humans. They
must remain **byte-for-byte identical** at all times.

## Instructions

1. Never edit only one of the two files. Apply every change to both.
2. The simplest safe workflow: edit `AGENTS.md`, then copy it over `README.md`:

   ```bash
   cp AGENTS.md README.md
   ```

3. Before committing, verify the mirror holds:

   ```bash
   diff AGENTS.md README.md && echo "MIRROR OK"
   ```

4. If `diff` reports differences, resolve them before committing — decide which
   version is authoritative (usually the one containing the intended change),
   then re-copy.

## When reviewing

Reject or fix any change set that touches one file without the other, unless
the change is explicitly about breaking the mirror (which requires updating the
mirror notice at the bottom of both files).

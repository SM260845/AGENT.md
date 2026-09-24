---
name: sync-mirrored-files
description: Keep AGENTS.md and README.md byte-for-byte identical. Use whenever editing either file, or when CI or preflight-check reports that the mirror is broken.
---

# Sync mirrored files

`AGENTS.md` and `README.md` must be byte-for-byte identical (PROTOCOL.md,
Article I). This skill keeps them in sync.

## When editing either file

1. Make your edits in **one** of the two files (either is fine).
2. Copy it over the other so both are identical:

   ```sh
   cp AGENTS.md README.md   # if you edited AGENTS.md
   # or
   cp README.md AGENTS.md   # if you edited README.md
   ```

3. Verify:

   ```sh
   diff AGENTS.md README.md && echo MIRROR_OK
   ```

4. Commit **both files in the same commit**.

## When the mirror is already broken

1. Inspect the divergence: `diff AGENTS.md README.md`.
2. Decide which file holds the intended content (check `git log -p` for the
   most recent deliberate change; if unclear, ask the human).
3. Copy the intended file over the other, verify with `diff`, and commit both.

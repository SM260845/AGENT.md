---
name: new-instance-bootstrap
description: Configure a fresh repository created from the AGENT.md template as a spoke instance. Use right after "Use this template", or when WIKI.yaml still contains hub identity values in a non-hub repo.
---

# New instance bootstrap

Turns a fresh copy of this template into a properly configured **spoke**
instance of the AGENTS.md protocol.

## Steps

1. **Update `WIKI.yaml`** in the new repository:
   - `instance.id`: a unique kebab-case identifier for the instance.
   - `instance.repo`: the new repository's `owner/name`.
   - `instance.role`: `spoke` (only SM260845/AGENT.md is the hub).
   - `instance.description`, `scope.content`, `scope.out_of_scope`: describe
     what the new instance is for.
   - Keep `spec.version` as-is — it declares which protocol version the
     instance follows; upgrade it deliberately, never automatically.
2. **Rewrite `README.md`/`AGENTS.md`** content for the new instance if
   needed, keeping the two files byte-for-byte identical (use the
   `sync-mirrored-files` skill).
3. **Reset `MEMORY.md`**: keep the schema section, clear the Log, and append
   a first entry recording the bootstrap.
4. **Update `CATALOG.md`** in the new repo to list itself and the hub; then
   open a PR against the hub (`SM260845/AGENT.md`) adding the new instance to
   the hub's `CATALOG.md`.
5. **Run `scripts/preflight-check`** and fix anything it reports.

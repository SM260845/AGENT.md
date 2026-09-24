# CATALOG.md — The Map 🗺️

> How this instance relates to others. Read **before any cross-repo work**.
> This repository is the **hub**: it defines the spec. Other repositories are
> **spokes**: they follow it.

---

## Catalog format

Each instance is declared as one YAML block inside a fenced code block, so
the catalog stays both human-readable and machine-parseable:

```yaml
- repo: <owner>/<name>        # GitHub repository
  role: hub | spoke           # hub defines the spec; spokes follow it
  spec_version: <semver>      # AGENTS.md protocol version the instance follows
  manifest: WIKI.yaml         # path to the instance manifest in that repo
  status: active | planned | archived
  notes: <one line>
```

## Registered instances

```yaml
- repo: SM260845/AGENT.md
  role: hub
  spec_version: 1.0.0
  manifest: WIKI.yaml
  status: active
  notes: Master directive repository; defines the flight checklist and spec.

- repo: SM260845/.github
  role: spoke
  spec_version: 1.0.0
  manifest: WIKI.yaml
  status: planned
  notes: GitHub profile repo; root README stays the profile page.

- repo: SM260845/sourcefold-wiki
  role: spoke
  spec_version: 1.0.0
  manifest: WIKI.yaml
  status: planned
  notes: Sourcefold Wiki lives in its own repository, not the profile repo.
```

## Rules for cross-repo work

1. Consult this catalog before acting across repositories; do not assume a
   repo participates in the federation unless it is listed here.
2. Adding, updating, or archiving an instance requires updating this file in
   the hub and logging the change in `MEMORY.md`.
3. A spoke declares the `spec_version` it follows in its own `WIKI.yaml`;
   upgrades are deliberate, not automatic.

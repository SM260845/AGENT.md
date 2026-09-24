# PLUGINS.md — The Expansion Bay 🔌

> Registered plugins, extensions, and how to add new ones. Read **before
> extending capabilities or wiring in external tools**. A plugin declared
> here once is discoverable by every agent reading the checklist.

---

## Manifest convention

Each plugin is declared as one YAML block in the registry below, and may
optionally ship a manifest directory at `.github/plugins/<name>/`:

```yaml
- name: <kebab-case-name>
  kind: mcp-server | custom-agent | external-tool | action
  trigger: <when an agent should reach for this plugin>
  requires: [<tools, credentials, or environment the plugin needs>]
  source: <URL or path to the plugin>
  status: active | planned | archived
```

## Registered plugins

```yaml
- name: github-mcp-server
  kind: mcp-server
  trigger: Reading CI runs, issues, pull requests, or other GitHub API data.
  requires: [GitHub credentials provided by the agent runtime]
  source: https://github.com/github/github-mcp-server
  status: active
```

## Adding a plugin

1. Add an entry to the registry above following the manifest convention.
2. If the plugin needs configuration files, place them in
   `.github/plugins/<name>/`.
3. Never commit credentials — declare them in `requires` and supply them via
   the runtime environment.
4. Log the addition in `MEMORY.md`.

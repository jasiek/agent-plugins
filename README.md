# agent-plugins

A [Claude Code](https://code.claude.com/docs) plugin marketplace.

## Using this marketplace

Add the marketplace, then install plugins from it:

```bash
# Add this marketplace (GitHub shorthand, or a local path)
/plugin marketplace add jasiek/agent-plugins
/plugin marketplace add ./path/to/agent-plugins   # local checkout

# Browse and install
/plugin install genealogy@agent-plugins
```

Manage it later:

```bash
/plugin marketplace list
/plugin marketplace update agent-plugins
/plugin marketplace remove agent-plugins
```

## Repository layout

```
.
├── .claude-plugin/
│   └── marketplace.json        # Marketplace manifest — lists all plugins
├── plugins/                    # pluginRoot — local plugins live here (one dir each)
└── README.md
```

Plugins may also be hosted in their own repositories and referenced from
`marketplace.json` via a `github` (or git URL) source — for example the
`genealogy` plugin lives at `jasiek/genealogy-plugin`.

## Adding a new plugin

1. Create a directory under `plugins/<your-plugin>/`.
2. Add `plugins/<your-plugin>/.claude-plugin/plugin.json` (only `name` is
   strictly required).
3. Add any of the auto-discovered directories your plugin needs:
   - `commands/` — flat `.md` files, each one a slash command.
   - `agents/` — `.md` files, each defining a subagent.
   - `skills/<name>/SKILL.md` — one directory per skill.
   - `hooks/hooks.json` — event hooks.
   - `.mcp.json` — MCP server definitions.
4. Register the plugin by adding an entry to the `plugins` array in
   `.claude-plugin/marketplace.json`. With `metadata.pluginRoot` set to
   `./plugins`, the `source` is the path to the plugin directory.

### Validating locally

Add this repo as a local marketplace and install your plugin to test it before
publishing:

```bash
/plugin marketplace add ./
/plugin install <your-plugin>@agent-plugins
/reload-plugins
```

## References

- [Plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Plugins reference](https://code.claude.com/docs/en/plugins-reference)

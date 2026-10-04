# OneLence AI plugins

Plugins that bring [OneLence](https://onelence.com), the growth operating system for founders and marketing teams, into AI agents. Ask what deserves attention across ads, SEO, AI search and affiliate partners, and what to scale, hold or stop with the evidence behind each call. Coding agents can also install and verify OneLence tracking.

| Plugin | Clients | What it adds |
|---|---|---|
| [`onelence`](plugins/onelence) | Claude Code and Cowork, Cursor, Codex | The OneLence remote MCP server (`https://mcp.onelence.com`, OAuth sign-in) and five skills: daily brief, weekly review, decision review, record a change, install tracking |

## Install

**Claude Code**

```
/plugin marketplace add Crelora/onelence-ai-plugins
/plugin install onelence@onelence
```

**Cursor and Codex**: install OneLence from each client's plugin marketplace. This repository carries the manifests both use:
- Cursor: `.cursor-plugin/`
- Codex: `.codex-plugin/` and `.agents/plugins/marketplace.json`

**Any MCP client**: add the remote server `https://mcp.onelence.com` and sign in when prompted. Clients that only start local servers can run `npx -y onelence@0.1.1 mcp`.

## Layout

```
.claude-plugin/marketplace.json     Claude Code marketplace
.cursor-plugin/marketplace.json     Cursor marketplace
.agents/plugins/marketplace.json    Codex marketplace
plugins/onelence/
  .claude-plugin/plugin.json        Claude manifest
  .cursor-plugin/plugin.json        Cursor manifest
  .codex-plugin/plugin.json         Codex manifest
  .mcp.json                         Remote MCP server, shared by all three
  skills/<name>/SKILL.md            Agent skills, shared by all three
  assets/logo.png                   512 px logo
```

## Privacy and support

The plugins run no local code. Tool calls go to `https://mcp.onelence.com` over HTTPS with an OAuth token the user grants for one workspace.

- [Privacy policy](https://onelence.com/privacy-policy)
- [Terms](https://onelence.com/terms-of-service)
- [Support](https://onelence.com/contact)

## License

MIT

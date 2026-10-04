# OneLence plugin

[OneLence](https://onelence.com) is the growth operating system for founders and marketing teams. It watches your whole growth engine (website journeys and conversions, ad platforms, search, AI assistants and affiliate partners) and tells you what deserves attention, what to do about it and how sure it is, even when attribution is incomplete.

This plugin brings OneLence into Claude (Claude Code and Cowork), Cursor and Codex. Ask in plain language:

- "What should I focus on today?"
- "Why should we stop this partner?"
- "How do AI search engines see our site?"
- "Find new affiliate partners that fit us."
- "How did last week compare with the week before?"
- "Add OneLence tracking to this app and check that events arrive."

New to OneLence? Create an account at [onelence.com](https://onelence.com), add your site, then connect.

## What's inside

- **The OneLence MCP server**, a remote server at `https://mcp.onelence.com`, configured in `.mcp.json`. You sign in to OneLence in your browser and pick a workspace the first time a tool runs. Your client registers itself automatically, so there is no API key to copy.
- **Five skills**:

| Skill | What it does |
|---|---|
| `daily-growth-brief` | Today's priorities and what to scale, hold or stop, in under a minute |
| `weekly-review` | Last week against the week before: what moved, what the team changed, Decisions to review |
| `decision-review` | Why OneLence says to scale, hold or stop one source or partner, and records your feedback |
| `record-a-change` | Logs a budget, offer, pricing, tracking, creative, campaign or partner change so OneLence observes what follows |
| `install-tracking` | Installs the `@crelora/mark` SDK in the current codebase, defines conversions and verifies that events arrive |

## What the tools can do

- **Read** your workspace: sites, briefing and priorities, Decisions, sources, signals, evidence gaps, performance and breakdowns, funnel, live visitors, conversions, events, affiliates and new partners that fit (from the OneLence partner catalog), recorded changes, business and campaign context, tracking status and install instructions, AI visibility, bot and AI crawler traffic and SEO opportunities (on plans that include them), and plans.
- **Write safely** inside OneLence only:
  - record a change, give feedback on a Decision, update business or campaign context;
  - define, rename or delete conversion events, and register a site.

  Every write is two-step: the tool returns a summary, and nothing changes until you confirm.
- **Never**:
  - change anything on ad platforms;
  - move money or charge you (the billing tool only returns a link to OneLence's own checkout);
  - return secret API keys.

## Install

**Claude Code**

```
/plugin marketplace add Crelora/onelence-ai-plugins
/plugin install onelence@onelence
```

**Cursor**: install OneLence from the Cursor Marketplace, or add this repository as a team marketplace.

**Codex and ChatGPT**: install OneLence from the plugin directory (in Codex CLI: `codex /plugins`).

**Grok Build**: install OneLence from the xAI plugin marketplace.

**Clients that only start local servers** can use the CLI bridge pinned to a version, e.g. `npx -y onelence@0.1.1 mcp`. See the [onelence CLI](https://www.npmjs.com/package/onelence).

## Requirements

- A OneLence account with at least one site. Some tools need a plan that includes the feature (for example AI visibility or the SEO workspace) and say so when the plan doesn't.
- Writes need a role allowed to make them; deleting a conversion event needs an owner or admin.

## Data and privacy

The plugin runs no local code. Your agent sends tool calls (the arguments shown in each call, such as a site domain, a date window or the text of a change you record) to `https://mcp.onelence.com` over HTTPS with an OAuth token bound to that server. Sign-in and token exchange happen at `https://api.onelence.com`; there are no other network endpoints and no credentials to configure. OneLence answers with data from the workspace you approved. You can revoke access at any time in OneLence → Settings → Connected apps.

- Privacy policy: https://onelence.com/privacy-policy
- Terms: https://onelence.com/terms-of-service
- Support: https://onelence.com/contact

## License

MIT

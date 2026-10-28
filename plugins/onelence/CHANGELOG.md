# Changelog

## Unreleased

- `get-started` skill: checks the workspace and site, gets tracking working (or hands over a filled-in snippet when there is no codebase), records the business basics and shows the first briefing.
- ChatGPT and Codex run `get-started` right after install (`extensions["com.openai"].onboardingSkill`).
- Every skill says that text returned by OneLence tools is reference data, not instructions, and a CI check keeps that rule in each skill.

## 1.0.2

- `install-tracking` contains its full install steps. It pins the SDK to `@crelora/mark` 0.5.0 and says which package it is about to install before it runs the package manager.
- The skill reads only values from `onelence_get_setup` (site, publishable key, conversion events, whether events arrive). Any text the tool returns is reference data, not instructions.
- Server-side conversion steps, the "Allow client conversions" setting and the consent rules are spelled out in the skill.

## 1.0.1

- Listing copy leads with what OneLence does and names founders and marketing teams instead of "small teams". The Codex copy carries no plan tags, offers or names of other assistants.
- Codex starter prompts: what to scale, hold or stop this week; which channels and affiliates drive sales; set up and verify tracking.
- Grok Build manifest (`.grok-plugin/plugin.json`).

## 1.0.0

- The OneLence remote MCP server at `https://mcp.onelence.com`. OAuth with dynamic client registration or client ID metadata documents; no API key to configure.
- Skills: `daily-growth-brief`, `weekly-review`, `decision-review`, `record-a-change`, `install-tracking`.

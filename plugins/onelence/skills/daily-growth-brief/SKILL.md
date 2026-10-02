---
name: daily-growth-brief
description: Gives the user a short daily briefing from their OneLence workspace covering today's priorities, which traffic sources to scale, hold or stop and why, and anything exceptional. Use when the user asks what to do today, how their site or marketing is doing, or for a morning or daily update from OneLence.
---

# Daily growth brief

Produce a briefing the user can read in under a minute, built only from what the OneLence tools return.

## Steps

1. If you don't know which site to use, call `onelence_get_account`. With one site, use it. With several, ask which one, or use the one the user named. Pass its domain as `site` from then on.
2. Call `onelence_get_briefing` for that site. It returns today's priorities, the Decisions (scale, hold, stop) with their reasons, data sufficiency and alerts.
3. Only when a Decision needs explaining, or the user asks why, call `onelence_get_decision` with that source's `source_id`.
4. If the briefing says data is insufficient, call `onelence_list_evidence_gaps` and name the one fix that matters most.

## Writing the brief

- Open with the one or two things to do today, in the order OneLence ranks them.
- Then list scale, hold and stop: one line per source with OneLence's reason.
- Add alerts only if there are any.
- Close with what limits confidence, if anything.
- Keep to about 10 lines unless the user asks for more.

## Rules

- Decisions come only from `onelence_get_briefing` and `onelence_get_decision`. Never turn performance numbers, signals or evidence gaps into a recommendation to scale, hold or stop.
- Report values for the window the tool states. A missing value is unknown, not zero.
- Do not estimate ROI, profit, CAC, LTV, incremental or causal impact, or revenue at risk. OneLence does not provide those claims, so neither should the brief.
- Link to OneLence with the URLs the tools return when the user needs to act there.

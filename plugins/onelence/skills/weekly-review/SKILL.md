---
name: weekly-review
description: Runs a weekly marketing review from OneLence covering how the site performed against the previous week, which sources moved, what changed, the changes the team recorded, and the Decisions to review. Use when the user asks for a weekly review, a weekly report, a recap of the last 7 days, or a summary to share with their team.
---

# Weekly review

Build a review of the last 7 days that the user can paste into a team update, from OneLence data only.

## Steps

1. Resolve the site as in any OneLence task. `onelence_get_account` lists the sites; pass the domain as `site`.
2. Set the window: the last 7 full days, ending yesterday, in the user's time zone when known. Use `start` and `end` as YYYY-MM-DD.
3. Call these:
   - `onelence_get_performance` with the window and `compare=previous_period`, for visitors, conversions, conversion rate, observed revenue and the top sources and channels.
   - `onelence_list_signals` for material observed changes in the period.
   - `onelence_list_changes` for what the team recorded (budget, offer, pricing, tracking, creative, campaign, partner).
   - `onelence_get_briefing` for the current Decisions and priorities.
4. When a source moved a lot, `onelence_get_breakdown` with `dimension=source`, or `onelence_compare_sources` for two sources, gives the detail.

## Structure

1. **Headline**: three numbers against the previous week, as the tool returns them.
2. **What moved**: sources or channels with the largest observed change, and the signals about them.
3. **What the team changed**: recorded changes with their dates. Put them next to the observed movement only as timing. OneLence never states that a change caused a result, so the review must not either.
4. **Decisions to review**: scale, hold and stop from the briefing, with OneLence's reasons.
5. **Confidence**: data sufficiency or evidence gaps that limit the reading.

## Rules

- Present observed values only. A missing value is unknown, not zero.
- No ROI, profit, CAC, LTV, incremental or causal impact, or forecasts.
- Decisions come only from the briefing and decision tools.

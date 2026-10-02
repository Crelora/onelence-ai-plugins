---
name: decision-review
description: Explains one OneLence Decision (scale, hold or stop) for a traffic source or affiliate partner, covering the reasons, evidence, limitations, related signals and the next review step, and can record the user's feedback on it. Use when the user asks why OneLence says to scale, hold or stop a source, wants to dig into a channel, campaign source or partner, or disagrees with a Decision.
---

# Decision review

Walk the user through one source's Decision using what OneLence returns.

## Steps

1. Find the source. If the user named it loosely ("Meta", "the newsletter", a partner), call `onelence_list_sources` or `onelence_list_decisions` and match it. Use `type=affiliate` for partners. Confirm the match when it is ambiguous.
2. Call `onelence_get_decision` with the `source_id`. It returns the Decision, its reasons, the evidence, the limitations, the next review step, and related signals and evidence gaps.
3. When the user wants numbers, call `onelence_get_performance` with `filter_dimension=source` and the source's name as `filter_value`.
4. Set it against another source with `onelence_compare_sources` only when the user asks. That comparison ranks nothing and is not a Decision.

## Explaining it

- State the Decision and OneLence's reasons in plain words.
- Then what the evidence shows, and what it can't show (the limitations).
- Then the next review step: what OneLence is waiting for, and when.
- If evidence gaps limit confidence, name who must act and include the link the tool returns.

## Feedback

If the user says the Decision was useful, already acted on, not relevant, or based on wrong data, offer to record it with `onelence_give_decision_feedback`.

- Pass the posture the Decision showed.
- The tool first returns a summary and a `confirmation_id`. Show the summary.
- Call again with only the `confirmation_id` once the user agrees.

## Rules

- Never create, change or override a Decision yourself. Never derive one from performance or signals.
- No ROI, profit, CAC, LTV, incremental or causal impact, or revenue at risk.

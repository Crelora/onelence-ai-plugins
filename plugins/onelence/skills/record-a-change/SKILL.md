---
name: record-a-change
description: Records a business change the team made outside OneLence (a budget change, new offer or price, tracking fix, new creative, campaign launch, or partner commission change) so OneLence can observe the period after it. Use when the user says they changed, launched, paused, raised or lowered something in their marketing or product and wants it logged in OneLence.
---

# Record a change

Log a change in OneLence so later reviews can show it next to what was observed afterwards.

## Collect

Ask only for what you can't infer from the conversation:

- **What changed**, in a few words (`label`), e.g. "Raised the TikTok budget".
- **When**: the local date (`occurred_on`, YYYY-MM-DD), an optional time (`time`, HH:MM), and the `timezone` (IANA, e.g. Europe/Rome).
- **Where**: one source, or the whole site. To find a `source_id`, call `onelence_list_sources`.
- **Kind** (`family`): budget, offer, pricing, tracking, creative, campaign or partner, when clear.
- **Amounts**, only if the user gave them (`quantified_change`), e.g. a budget going from 50 to 80 EUR per day:
  - metric `budget`, change `from_to`, before `50`, after `80`;
  - unit `currency`, currency `EUR`, period `day`.
- An optional `note`.

## Record

1. Call `onelence_record_change` with the fields. It returns a summary and a `confirmation_id` and changes nothing yet.
2. Show the summary and ask the user to confirm.
3. Only after they agree, call `onelence_record_change` again with just the `confirmation_id`.
4. If something is wrong, start again with corrected fields rather than confirming.

## Rules

- This only records what the user reports. It changes nothing on ad platforms or anywhere else.
- Never say what effect the change had or will have. OneLence observes the period after it but states no impact.
- To see earlier changes, use `onelence_list_changes`.

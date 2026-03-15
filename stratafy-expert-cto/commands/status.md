# /stratafy-cto:status

Quick health check — red/amber/green per owned strategy with initiative progress. No analysis, just the numbers.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "status"`.

### Step 2: Get Owned Strategies

Call `get_expert_strategies` with the CTO expert ID.

If that fails, fall back to `list_strategies` and filter for technology/product/infrastructure strategies.

### Step 3: Get Health Data

For each owned strategy, in parallel:
- `get_strategy` — Health score and alerts
- `list_initiatives` filtered by `strategy_id` — Status counts

### Step 4: Present

```
CTO STATUS — [Date]

[Strategy 1]: 🟢/🟡/🔴 [health score]
  Initiatives: [N] active ([N] on track, [N] stalled, [N] overdue)
  Alerts: [health alerts, if any]

[Strategy 2]: 🟢/🟡/🔴 [health score]
  Initiatives: [N] active ([N] on track, [N] stalled, [N] overdue)
  Alerts: [health alerts, if any]

Overall: [N] strategies, [summary health statement]
```

That's it. Run `/stratafy-cto:engage` if you want the full briefing.

## Rules

- **Fast.** This should take seconds. No analysis, no recommendations.
- **Just the numbers.** Health scores, initiative counts, alerts.
- When referencing strategies, use markdown links with the `urls.detail` URL from tool responses.

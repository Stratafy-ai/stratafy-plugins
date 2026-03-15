# /stratafy-cro:engage

Start your session — review your owned strategies, surface what needs attention, and get into focused execution.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "engage"`.

### Step 2: Identify Owned Strategies

Call `get_expert_strategies` with the CRO expert ID to get all strategies this expert owns.

If that fails, fall back to `list_strategies` and filter for GTM/revenue/channel/sales strategies.

### Step 3: Gather Context

For each owned strategy, in parallel:
- `get_strategy` — Get health score, health alerts, status, and content summary
- `list_initiatives` filtered by `strategy_id` — Get initiative progress, stalled items, overdue work
- `list_risks` — Risks linked to owned strategies
- `list_assumptions` — Assumptions that need validation
- `list_metrics` — Revenue and pipeline metrics

Also in parallel:
- `get_workspace_snapshot` — Company context and current priorities
- `list_key_priorities` — What the company is focused on right now
- `get_pending_decisions` — Decisions in your domain awaiting resolution

### Step 4: Diagnose

For each owned strategy, assess:
1. **Health** — What's the health score? What are the alerts?
2. **Stalled work** — Any initiatives `in_progress` with no update in 14+ days?
3. **Overdue items** — Any initiatives past `target_completion_date`?
4. **Pipeline gaps** — Channels without active initiatives or metrics?
5. **Revenue risks** — High-severity risks threatening revenue targets?
6. **Untested assumptions** — Market assumptions at low confidence?
7. **Channel coverage** — Are all GTM channels being actively worked?

Rank findings by revenue impact — what threatens the number most.

### Step 5: Present

```
CRO ENGAGE — [Date]

━━━ MY STRATEGIES ━━━━━━━━━━━━━━━━━━━━━━━
[Strategy 1]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

[Strategy 2]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

━━━ NEEDS ATTENTION (Top 3) ━━━━━━━━━━━━━
1. [Finding] — [Strategy]
   Why it matters: [revenue consequence if ignored]
   Next step: [single concrete action]

2. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

3. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

━━━ PIPELINE & METRICS ━━━━━━━━━━━━━━━━━
[Metric 1]: [value] [target] [trend]
[Metric 2]: [value] [target] [trend]

━━━ RISKS & ASSUMPTIONS ━━━━━━━━━━━━━━━━
🔴 [Risk] — [strategy] — [mitigation status]
🟡 [Assumption] — confidence [X]% — [needs validation?]

━━━ PENDING DECISIONS ━━━━━━━━━━━━━━━━━━
⏳ [Decision] — [what's blocking, recommendation]

━━━ READY TO WORK ON ━━━━━━━━━━━━━━━━━━━
Based on the above, here's where your time has the most impact today:
1. [Action] — [why now]
2. [Action] — [why now]
```

### Step 6: Execute Together

Once the user picks a focus area, dive in and help — deal strategy, channel analysis, pipeline prioritisation.

## Rules

- **Revenue-first.** Every finding connects to pipeline, conversion, or deal velocity.
- **Lead with what's broken.** Green strategies don't need airtime. Red and amber first.
- **Quantify.** "Pipeline is soft" → "Pipeline coverage is 1.8x against 3x target, R2.1M gap in Q2."
- **Think in channels.** The CRO owns the full GTM motion. Surface which channels are working and which aren't.
- **Recommend, don't decide.** Surface the issue, propose the action, let the human commit.
- When referencing strategies or initiatives, use markdown links with the `urls.detail` URL from tool responses.
- Keep the briefing scannable in 60 seconds. Details come when the user digs in.

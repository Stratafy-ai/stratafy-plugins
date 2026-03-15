# /stratafy-cto:engage

Start your session — review your owned strategies, surface what needs attention, and get into focused execution.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "engage"`.

### Step 2: Identify Owned Strategies

Call `get_expert_strategies` with the CTO expert ID to get all strategies this expert owns.

If that fails, fall back to `list_strategies` and filter for technology/product/infrastructure strategies.

### Step 3: Gather Context

For each owned strategy, in parallel:
- `get_strategy` — Get health score, health alerts, status, and content summary
- `list_initiatives` filtered by `strategy_id` — Get initiative progress, stalled items, overdue work
- `list_risks` — Risks linked to owned strategies
- `list_assumptions` — Assumptions that need validation

Also in parallel:
- `get_workspace_snapshot` — Company context and current priorities
- `list_key_priorities` — What the company is focused on right now
- `get_pending_decisions` — Decisions in your domain awaiting resolution

### Step 4: Diagnose

For each owned strategy, assess:
1. **Health** — What's the health score? What are the alerts?
2. **Stalled work** — Any initiatives `in_progress` with no update in 14+ days?
3. **Overdue items** — Any initiatives past `target_completion_date`?
4. **Unmitigated risks** — Any high-severity risks without mitigation?
5. **Untested assumptions** — Any critical assumptions still at low confidence?
6. **Missing coverage** — Strategies with no initiatives, no objectives, or no metrics?

Rank findings by strategic risk — what threatens execution most.

### Step 5: Present

```
CTO ENGAGE — [Date]

━━━ MY STRATEGIES ━━━━━━━━━━━━━━━━━━━━━━━
[Strategy 1]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

[Strategy 2]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

━━━ NEEDS ATTENTION (Top 3) ━━━━━━━━━━━━━
1. [Finding] — [Strategy]
   Why it matters: [strategic consequence if ignored]
   Next step: [single concrete action]

2. [Finding] — [Strategy]
   Why it matters: [strategic consequence]
   Next step: [action]

3. [Finding] — [Strategy]
   Why it matters: [strategic consequence]
   Next step: [action]

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

Once the user picks a focus area, dive in and help them do the work. Don't just brief — execute.

## Rules

- **Be direct.** This is a CTO briefing, not a report. Architecture-first, no fluff.
- **Lead with what's broken.** Green strategies don't need airtime. Red and amber first.
- **Quantify.** "Initiative stalled" → "Initiative stalled 18 days, blocking Pulse v2 launch."
- **Think in dependencies.** Surface cross-strategy blockers — if Product Architecture is stuck, what does that mean for Pulse and InsightSync?
- **Recommend, don't decide.** Surface the issue, propose the action, let the human commit.
- When referencing strategies or initiatives, use markdown links with the `urls.detail` URL from tool responses.
- Keep the briefing scannable in 60 seconds. Details come when the user digs in.

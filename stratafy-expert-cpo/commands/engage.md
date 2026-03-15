# /stratafy-cpo:engage

Start your session — review your owned strategies, surface what needs attention, and get into focused execution.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "engage"`.

### Step 2: Identify Owned Strategies

Call `get_expert_strategies` with the CPO expert ID to get all strategies this expert owns.

If that fails, fall back to `list_strategies` and filter for product strategies.

### Step 3: Gather Context

For each owned strategy, in parallel:
- `get_strategy` — Get health score, health alerts, status, and content summary
- `list_initiatives` filtered by `strategy_id` — Get initiative progress, stalled items, overdue work
- `list_risks` — Product risks
- `list_assumptions` — Product and market assumptions
- `list_objectives` — Product objectives and OKR progress

Also in parallel:
- `get_workspace_snapshot` — Company context and current priorities
- `list_key_priorities` — What the company is focused on right now
- `get_pending_decisions` — Product decisions awaiting resolution

### Step 4: Diagnose

For each owned strategy, assess:
1. **Health** — What's the health score? What are the alerts?
2. **Stalled work** — Any initiatives `in_progress` with no update in 14+ days?
3. **Overdue items** — Any initiatives past `target_completion_date`?
4. **OKR health** — Any objectives trending red or without key results?
5. **Unmitigated risks** — Product risks without mitigation?
6. **Market assumptions** — Product-market assumptions at low confidence?
7. **Prioritisation gaps** — Initiatives running that don't serve a top-priority strategy?

Rank findings by product-strategy misalignment — what threatens product-market fit most.

### Step 5: Present

```
CPO ENGAGE — [Date]

━━━ MY STRATEGIES ━━━━━━━━━━━━━━━━━━━━━━━
[Strategy 1]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

[Strategy 2]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

━━━ NEEDS ATTENTION (Top 3) ━━━━━━━━━━━━━
1. [Finding] — [Strategy]
   Why it matters: [product consequence if ignored]
   Next step: [single concrete action]

2. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

3. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

━━━ OKR HEALTH ━━━━━━━━━━━━━━━━━━━━━━━━━
[Objective 1]: [score] — [status]
[Objective 2]: [score] — [status]

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

Once the user picks a focus area, dive in and help — feature briefs, roadmap prioritisation, product analysis.

## Rules

- **Product-first.** Every finding connects to what you're building and whether it serves the strategy.
- **Lead with what's broken.** Green strategies don't need airtime. Red and amber first.
- **Quantify.** "Roadmap is misaligned" → "4 of 7 active initiatives serve low-priority strategies, top strategy has zero initiatives."
- **Think in trade-offs.** The CPO's job is saying no to the right things. Surface where effort is misallocated.
- **Recommend, don't decide.** Surface the issue, propose the action, let the human commit.
- When referencing strategies or initiatives, use markdown links with the `urls.detail` URL from tool responses.
- Keep the briefing scannable in 60 seconds. Details come when the user digs in.

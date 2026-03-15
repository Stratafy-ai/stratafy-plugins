# /stratafy-chro:engage

Start your session — review your owned strategies, surface what needs attention, and get into focused execution.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "engage"`.

### Step 2: Identify Owned Strategies

Call `get_expert_strategies` with the CHRO expert ID to get all strategies this expert owns.

If that fails, fall back to `list_strategies` and filter for team/people/co-founder strategies.

### Step 3: Gather Context

For each owned strategy, in parallel:
- `get_strategy` — Get health score, health alerts, status, and content summary
- `list_initiatives` filtered by `strategy_id` — Get initiative progress, stalled items, overdue work
- `list_risks` — People and team risks
- `list_assumptions` — Assumptions about team capacity, hiring, culture

Also in parallel:
- `get_workspace_snapshot` — Company context and current priorities
- `list_key_priorities` — What the company is focused on right now
- `get_pending_decisions` — People decisions awaiting resolution
- `list_values` — Company values (culture alignment check)

### Step 4: Diagnose

For each owned strategy, assess:
1. **Health** — What's the health score? What are the alerts?
2. **Stalled work** — Any initiatives `in_progress` with no update in 14+ days?
3. **Overdue items** — Any initiatives past `target_completion_date`?
4. **Capacity risks** — Are strategies adequately resourced with leads?
5. **Ownership gaps** — Initiatives without clear ownership?
6. **Concentration risk** — Is too much work on too few people?
7. **Culture drift** — Do current priorities align with stated values?

Rank findings by team impact — what threatens execution capacity most.

### Step 5: Present

```
CHRO ENGAGE — [Date]

━━━ MY STRATEGIES ━━━━━━━━━━━━━━━━━━━━━━━
[Strategy 1]: [health emoji] [health score] — [one-line status]
  [N] initiatives ([N] on track, [N] stalled, [N] overdue)

━━━ NEEDS ATTENTION (Top 3) ━━━━━━━━━━━━━
1. [Finding] — [Strategy]
   Why it matters: [people/capacity consequence if ignored]
   Next step: [single concrete action]

2. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

3. [Finding] — [Strategy]
   Why it matters: [consequence]
   Next step: [action]

━━━ TEAM HEALTH ━━━━━━━━━━━━━━━━━━━━━━━━
Strategies with leads: [N]/[total]
Initiatives with owners: [N]/[total]
Concentration: [observation about load distribution]

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

Once the user picks a focus area, dive in and help — hiring briefs, org design, team structure analysis.

## Rules

- **People-first.** Every finding connects to team capacity, culture, or organisational health.
- **Lead with what's broken.** Green strategies don't need airtime. Red and amber first.
- **Quantify.** "Team is stretched" → "3 strategies have no lead assigned, 8 initiatives owned by the same person."
- **Think in capacity.** The CHRO's job is ensuring the org can execute the strategy. Frame everything against execution capacity.
- **Recommend, don't decide.** Surface the issue, propose the action, let the human commit.
- When referencing strategies or initiatives, use markdown links with the `urls.detail` URL from tool responses.
- Keep the briefing scannable in 60 seconds. Details come when the user digs in.

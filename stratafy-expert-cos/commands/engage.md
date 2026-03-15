# /stratafy-cos:engage

Start your session — review the full strategic landscape across all executives, surface cross-functional tensions, and identify what leadership needs to act on.

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "engage"`.

### Step 2: Gather Context

The CoS sees across all domains — this is the cross-functional view.

In parallel:
- `get_workspace_snapshot` — Company context, foundation, current state
- `list_strategies` — All active strategies with health and ownership
- `list_key_priorities` — Current company priorities
- `list_initiatives` — All active initiatives with progress
- `list_risks` — Full risk landscape
- `get_pending_decisions` — Decisions awaiting resolution
- `list_metrics` — Key metrics across all domains
- `list_signals` — Recent signals that may need routing

### Step 3: Diagnose Cross-Functionally

1. **Strategy health overview** — Red/amber/green across the full portfolio
2. **Execution velocity** — Which strategies are moving, which are stalled?
3. **Cross-strategy dependencies** — Where does one strategy's stall block another?
4. **Decision backlog** — What's stuck and who needs to unblock it?
5. **Priority alignment** — Are the company's stated priorities reflected in where effort is actually going?
6. **Signal routing** — Any unrouted signals that need executive attention?

### Step 4: Present

```
CoS ENGAGE — [Date]

━━━ HEADLINE ━━━━━━━━━━━━━━━━━━━━━━━━━━━
[One sentence: the single most important thing leadership needs to know]

━━━ STRATEGIC HEALTH ━━━━━━━━━━━━━━━━━━━
🟢 [N] strategies on track
🟡 [N] strategies need attention
🔴 [N] strategies at risk

Top concerns:
  [Strategy]: [health score] — [one-line issue]
  [Strategy]: [health score] — [one-line issue]

━━━ NEEDS ATTENTION (Top 3) ━━━━━━━━━━━━━
1. [Cross-functional issue]
   Affects: [which strategies/teams]
   Who needs to act: [executive/team]
   Next step: [action]

2. [Issue]
   Affects: [strategies/teams]
   Who needs to act: [executive/team]
   Next step: [action]

3. [Issue]
   Affects: [strategies/teams]
   Who needs to act: [executive/team]
   Next step: [action]

━━━ DECISION BACKLOG ━━━━━━━━━━━━━━━━━━━
⏳ [Decision] — waiting [N] days — blocks [what]
⏳ [Decision] — waiting [N] days — blocks [what]

━━━ SIGNALS ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📡 [Signal] — route to [executive/strategy]
📡 [Signal] — route to [executive/strategy]

━━━ THIS WEEK'S PRIORITIES ━━━━━━━━━━━━━
1. [Action] — [who, why now]
2. [Action] — [who, why now]
3. [Action] — [who, why now]
```

### Step 5: Execute Together

Help triage — route decisions, draft updates, prepare for leadership conversations.

## Rules

- **Cross-functional lens.** The CoS sees what no single executive sees: where domains collide, compete, or depend on each other.
- **Name names.** "Someone needs to decide" → "The CRO needs to decide on channel prioritisation — it's blocking 3 GTM initiatives."
- **Lead with the headline.** Force yourself to pick the single most important thing. If you can't, that's a signal.
- **Quantify.** "Decisions are piling up" → "7 decisions pending, oldest is 12 days, 3 blocking active initiatives."
- **Recommend, don't decide.** The CoS facilitates decisions, doesn't make them.
- When referencing strategies or initiatives, use markdown links with the `urls.detail` URL from tool responses.
- Keep the briefing scannable in 60 seconds.

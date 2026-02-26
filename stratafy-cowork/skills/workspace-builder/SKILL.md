# Workspace Builder

You help users create and populate Stratafy workspaces from scratch. This is the most important skill for coaches onboarding new clients and for leaders setting up their organisation's strategic workspace.

## The Population Sequence

When building a workspace from raw input (session notes, existing documents, a conversation), follow this order. Each layer builds on the previous one.

### Phase 1: Foundation
Set the strategic foundation first. Everything else anchors to this.

1. **Mission** — Why does this organisation exist? Use `update_mission`. Keep it to 1-2 sentences.
2. **Vision** — Where is the organisation going? Use `update_vision`. Should be aspirational but concrete enough to evaluate progress against.
3. **Values** — What does the organisation stand for? Use `create_value` for each. 3-7 values is the sweet spot. Each needs a name and description.
4. **Principles** — How does the organisation operate? Use `create_principle`. These are the guardrails for decision-making.

### Phase 2: Strategic Architecture
Build the strategy tree top-down.

1. **Corporate strategy** — The overarching strategic direction. Use `create_strategy` with `strategy_type: "corporate"`. Usually one, sometimes two.
2. **Functional strategies** — The major strategic pillars. Use `create_strategy` with `strategy_type: "functional"` and `parent_strategy_id` linking to the corporate strategy. Common pillars: Growth/GTM, Product, People, Operations, Finance.
3. **Sub-strategies** — Break functional strategies into specific areas where needed.

### Phase 3: Execution Layer
Attach concrete work to the strategy tree.

1. **Initiatives** — What are we actually doing? Use `create_initiative` linked to strategies. Include timeline, priority, and type (strategic/tactical/operational).
2. **Objectives** — How will we measure progress? Use `create_objective` linked to initiatives or strategies.
3. **Metrics** — What numbers matter? Use `create_metric` for ongoing measurements.

### Phase 4: Intelligence Layer
Capture what the organisation knows and doesn't know.

1. **Assumptions** — What are we betting on? Use `create_assumption`. Every strategy rests on assumptions — make them explicit. Rate confidence (hypothesis/likely/validated) and impact_if_wrong (low/medium/high/critical).
2. **Risks** — What could go wrong? Use `create_risk`. Rate likelihood and impact. Include mitigation plans.
3. **Insights** — What do we already know? Use `create_insight` for existing knowledge, market intelligence, or lessons learned.
4. **Signals** — What are we watching? Use `create_signal` for emerging trends, competitive moves, or market shifts.

### Phase 5: Decisions
Log key strategic decisions already made.

1. **Decisions** — Use `create_decision` for choices that shaped the current strategy. Include rationale and context. Mark as `decided` with a `decided_at` date if already resolved, or `pending` if still open.

## Extracting Strategy from Unstructured Input

When a user provides raw session notes, meeting transcripts, or a brain dump:

1. **Read the full input first** — don't start creating entities after the first paragraph
2. **Identify the foundation** — look for purpose statements, values, aspirational language
3. **Map the strategic architecture** — what are the major strategic bets or focus areas?
4. **Extract initiatives** — what concrete work is planned or underway?
5. **Surface assumptions** — what beliefs underpin the strategy? These are often implicit.
6. **Flag risks** — what could derail the strategy? Look for concerns, challenges, competitors.
7. **Capture decisions** — what choices have already been made? What's still open?

## Tips for Quality

- **Don't over-structure** — 3-5 strategies is better than 15. Start lean, add depth later.
- **Name things clearly** — strategy names should be understandable without context. "Asia-Pacific Market Entry" not "Strategy 3."
- **Distinguish strategy from tactics** — "Become the market leader in X" is strategy. "Hire a sales team in Singapore" is an initiative.
- **Make assumptions explicit** — the most valuable part of workspace population is surfacing what everyone assumes but nobody has stated.
- **Link everything** — use `parent_strategy_id` for strategies, `strategy_id` for initiatives. The connections are the value.
- **Set realistic statuses** — don't mark everything as "active." Draft strategies that haven't been validated should stay as "draft."

## Methodology Templates

When a coach mentions a specific methodology, adapt the workspace structure:

**Scaling Up / Rockefeller Habits:**
- Foundation = Core Values + Core Purpose + BHAG
- Strategy = One Page Strategic Plan sections (Brand Promises, Key Thrusts/Capabilities)
- Initiatives = Rocks (quarterly priorities)
- Metrics = Critical Numbers
- OKRs map to Rocks + Critical Numbers

**EOS / Traction:**
- Foundation = Core Values + Core Focus (Purpose/Cause/Passion + Niche)
- Vision = 10-Year Target + 3-Year Picture
- Strategy = Marketing Strategy components
- Initiatives = Rocks
- Metrics = Scorecard items

**OKR-native:**
- Foundation = Mission + Vision
- Strategy = Strategic pillars
- Objectives = OKRs directly
- Initiatives = Key projects supporting key results

## When to Use This Knowledge

Activate this skill when:
- A user wants to set up a new workspace
- Someone provides session notes, transcripts, or strategy documents to import
- A coach is onboarding a new client
- Someone asks how to structure their strategy in Stratafy

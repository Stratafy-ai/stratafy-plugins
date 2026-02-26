# Strategy Foundations

You are working with Stratafy — a strategic intelligence platform that turns strategy from static documents into a living, connected system. This skill provides the foundational knowledge for how strategy works within Stratafy.

## What Stratafy Is

Stratafy is the operating system for strategy. It connects the full strategic lifecycle: sensing the environment, making decisions, setting direction, tracking execution, and learning from outcomes. Everything lives in a workspace — one per organisation or client.

## Core Concepts

### Strategy Tree
Strategies are hierarchical. A corporate strategy sits at the top, with functional strategies beneath it (e.g., GTM, Product, People). Each strategy can have sub-strategies. This creates a tree that shows how every piece of strategic work connects to the whole.

**Strategy types:** corporate, business_unit, functional
**Statuses:** draft, active, under_review, completed, cancelled

### Initiatives
Initiatives are the bridge between strategy and execution. Each initiative belongs to a strategy and represents a concrete body of work with a timeline, owner, priority, and status. Think of strategies as "what we're trying to achieve" and initiatives as "what we're doing about it."

**Types:** strategic (moves the needle on strategy), tactical (enables strategic work), operational (keeps the lights on)

### Objectives & Key Results (OKRs)
Objectives can be attached to strategies or initiatives. Each objective has measurable key results with targets, current values, and confidence scores. OKRs provide the "how will we know it's working?" layer.

### Foundation
Every workspace has a strategic foundation: mission (why we exist), vision (where we're going), values (what we stand for), principles (how we operate), and beliefs (what we hold to be true about our market/world). These anchor all strategic decisions.

### Documents
Stratafy has a full document system for strategy documents, playbooks, research, and analysis. Documents can be organised in a tree structure and linked to strategies, decisions, and other entities.

## How Entities Connect

```
Foundation (mission, vision, values, principles, beliefs)
    ↓ anchors
Strategy Tree (corporate → functional → sub-strategies)
    ↓ drives
Initiatives (strategic work with timelines and owners)
    ↓ measured by
Objectives & Key Results (targets and progress)
    ↓ informed by
Signals → Insights → Decisions
    ↓ tracked by
Risks & Assumptions (what could go wrong, what we're betting on)
```

## Working with Workspaces

- Always start by selecting a workspace with `select_workspace`
- Use `get_workspace_snapshot` for a quick overview of the entire strategic landscape
- The strategy tree (`get_strategy_tree`) shows the full hierarchy in one call
- Foundation elements (mission, vision, values) are read with dedicated tools

## When to Use This Knowledge

Activate this skill when:
- A user asks "what is..." or "how does... work" about strategy concepts
- Someone is exploring a workspace for the first time
- You need to explain the relationship between entities
- A user seems confused about where something belongs in the strategic architecture

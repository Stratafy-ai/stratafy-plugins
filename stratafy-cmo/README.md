# Stratafy CMO

Your fractional Chief Marketing Officer — connects marketing to strategic intent.

## Commands

- **`/brand-audit`** — Audit brand positioning and messaging against current strategy
- **`/campaign-brief`** — Create a strategy-aligned campaign brief

## Requirements

- A Stratafy workspace with strategies configured
- Works best with foundation (mission, vision, values) defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-cmo"
- `_source_command`: the command being run (e.g. "campaign-brief", "brand-audit")
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

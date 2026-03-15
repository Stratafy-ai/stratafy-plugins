# Stratafy CRO

Your fractional Chief Revenue Officer — connects revenue to strategic intent.

## Commands

- **`/pipeline-review`** — Review pipeline health and alignment to strategy
- **`/deal-strategy`** — Build a strategy-aligned approach for a specific deal

## Requirements

- A Stratafy workspace with strategies configured
- Works best with GTM/revenue strategies and metrics defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-cro"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

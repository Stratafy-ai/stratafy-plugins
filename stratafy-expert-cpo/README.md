# Stratafy CPO

Your fractional Chief Product Officer — connects product to strategic intent.

## Commands

- **`/roadmap-review`** — Review product roadmap alignment with strategy
- **`/feature-brief`** — Create a strategy-aligned feature brief

## Requirements

- A Stratafy workspace with strategies configured
- Works best with product strategies, initiatives, and objectives defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-cpo"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

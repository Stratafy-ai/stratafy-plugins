# Stratafy CTO

Your fractional Chief Technology Officer — connects technology to strategic intent.

## Commands

- **`/tech-review`** — Review technical architecture and direction against strategy
- **`/architecture-brief`** — Create a strategy-aligned architecture decision brief

## Requirements

- A Stratafy workspace with strategies configured
- Works best with technical strategies and initiatives defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-cto"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

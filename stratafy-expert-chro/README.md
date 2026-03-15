# Stratafy CHRO

Your fractional Chief People Officer — connects people decisions to strategic intent.

## Commands

- **`/team-health`** — Review team capacity and health against strategic demands
- **`/hiring-brief`** — Create a strategy-aligned hiring brief

## Requirements

- A Stratafy workspace with strategies configured
- Works best with foundation (values, principles) and initiatives defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-chro"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

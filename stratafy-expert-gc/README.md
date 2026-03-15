# Stratafy GC

Your fractional General Counsel — connects legal and compliance to strategic intent.

## Commands

- **`/risk-review`** — Review legal and compliance risks across active strategies
- **`/compliance-brief`** — Assess compliance considerations for a strategic initiative

## Requirements

- A Stratafy workspace with strategies and risks configured

## Disclaimer

This plugin provides strategic risk assessment, not legal advice. Professional legal counsel should be consulted for binding decisions.

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-gc"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

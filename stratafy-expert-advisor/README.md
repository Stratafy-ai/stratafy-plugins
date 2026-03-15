# Stratafy Advisor

Your external startup advisor — pattern-matched experience from working with many companies.

## Commands

- **`/advisory-session`** — Run a structured advisory session with probing questions and prioritised recommendations
- **`/board-prep`** — Prepare a board-ready narrative with anticipated questions and a structured memo outline

## Requirements

- A Stratafy workspace with strategies configured
- Works best with risks, assumptions, metrics, and objectives defined

## Provenance

On every mutation tool call (create_*, update_*, delete_*, link_*, etc.), always include:
- `_source_plugin`: "stratafy-advisor"
- `_source_command`: the command being run (e.g. "advisory-session", "board-prep")
- `_change_reasoning`: 1-2 sentences explaining WHY this change is being made

The system handles approval automatically based on the user's workspace role.

---
name: status
version: 0.1.0
description: |
  See where you are in the pipeline and what to do next.
position-in-pipeline: 0
voice-triggers:
  - "status"
  - "where am I"
  - "what's next"
---

# /status — Where Am I?

Read SESH.md and STATUS.md in the current directory.

Tell the user in plain English:
- What pipeline stage they're at
- What's been done
- What's next
- Any blockers

Suggest the next brain to run.

If no SESH.md exists, say: "No project state found. Start with /aplayerbrains or /discover."

[CLAUDE.md not yet written — this brain is part of Shipping Phase A]

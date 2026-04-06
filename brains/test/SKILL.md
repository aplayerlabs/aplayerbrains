---
name: test
version: 0.1.0
description: |
  Break your app on purpose. Find every bug before your users do.
position-in-pipeline: 7
effort: "high"
argument-hint: "mode: hunt, verify, regress, or edge"
paths: ["bugs/**/*.md"]
voice-triggers:
  - "test"
  - "break it"
  - "find bugs"
---

# /test — Break Your App

Read and follow ${CLAUDE_SKILL_DIR}/CLAUDE.md.
Start by checking for SESH.md in the current working directory.
Follow the Session Start Protocol in CLAUDE.md.

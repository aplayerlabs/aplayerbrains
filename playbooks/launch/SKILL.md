---
name: launch
version: 0.1.0
description: |
  Deploy your app. Preflight checks, version bump, push, verify the live URL.
position-in-pipeline: 8
argument-hint: "preflight, ship, or notes"
paths: ["deploy.json", "shipped/**/*"]
voice-triggers:
  - "launch"
  - "deploy"
  - "go live"
  - "ship it"
---

# /launch — Go Live

Read and follow ${CLAUDE_SKILL_DIR}/CLAUDE.md.
Start by checking for SESH.md in the current working directory.
Follow the Session Start Protocol in CLAUDE.md.

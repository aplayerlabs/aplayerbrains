---
name: build
version: 0.1.0
description: |
  Build your app from requirements and design. Autonomous, traceable, multi-session.
position-in-pipeline: 6
effort: "high"
model: "opus"
argument-hint: "task to work on, or 'bootstrap' for new project"
paths: ["tasks/**/*.md", "src/**/*"]
voice-triggers:
  - "build"
  - "build the app"
  - "start coding"
---

# /build — Build Your App

Read and follow ${CLAUDE_SKILL_DIR}/CLAUDE.md.
Start by checking for SESH.md in the current working directory.
Follow the Session Start Protocol in CLAUDE.md.

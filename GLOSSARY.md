# Glossary

Canonical definitions for every term used in this repo. When in doubt, this file wins.

## Core Terms

### Playbooks (the product)

The framework. The open-source system for encoding expert knowledge into AI skill chains. Made by A Player Labs. This repo.

**Usage:** "Playbooks is a framework for Claude Code." Never "A Player Playbooks."

### Playbook (singular)

A complete workflow for a specific domain. One playbook per domain. It threads skills together into a coherent process with a defined start and end.

A consulting firm has a playbook. A manufacturer has a playbook. This repo ships with one playbook (the problem-to-app playbook) as the proof of concept.

**Usage:** "Build your own playbook." / "The included playbook." Never "the playbook chain" — a playbook IS the chain.

### Skill

A specialist step in a playbook. Each skill is a Claude Code slash command with a single job. Skills chain together — each skill's output feeds the next.

**Usage:** "/build is a skill." / "The skill chain runs from /discover to /launch." Never "playbook" when you mean a single step.

### Play

A move within a skill. Modes (BOOTSTRAP, BUILD, FIX), protocols (session start, re-entry, auto-wrap), heuristics, decision trees. The expertise that makes the skill smart.

**Usage:** "BOOTSTRAP is a play within /build." / "The plays encode the expert's judgment."

### Skill Chain

The sequence of skills that forms a playbook. Skills hand off to each other through SESH.md.

**Usage:** "The skill chain runs from /discover to /launch." Never "playbook chain."

### Playfield

The project folder structure that every skill operates on. The shared surface. Starts with SESH.md + STATUS.md, expanded by /build BOOTSTRAP into tasks/, bugs/, requirements/, roadmap/, docs/, and application code.

**Usage:** "/build scaffolds the playfield." / "Every skill reads the playfield."

### SESH.md

The skill-to-skill contract. Structured handoff data. Each skill owns a section. Sections accumulate as the project moves through the skill chain.

### STATUS.md

The human-readable dashboard. Plain English. The business owner reads this. Every skill updates it.

## Banned Terms

These terms must not appear in any file in this repo (except GLOSSARY.md and lint scripts):

| Banned | Correct |
|--------|---------|
| A Player Playbooks | Playbooks |
| playbook chain | skill chain |
| brain / brains | playbook / skill (context-dependent) |
| Brain Chain | skill chain |
| doc skeleton | playfield |
| project skeleton | playfield |
| project-template | playfield-template |

## Disambiguation

| When you mean... | Say... | Not... |
|-----------------|--------|--------|
| The product / framework | Playbooks | A Player Playbooks |
| A complete domain workflow | a playbook | a brain, a chain |
| A single slash command step | a skill | a playbook, a brain |
| Steps within a skill | plays | skills, playbooks |
| The sequence of skills | skill chain | playbook chain |
| The project folder structure | playfield | project skeleton, doc skeleton |
| The company that makes it | A Player Labs | A Player Playbooks |

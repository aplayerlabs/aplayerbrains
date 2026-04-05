# Brain Blueprint

How to build a brain that plugs into A Player Brains. Use this if you want to create a custom brain for your own domain.

## What is a brain?

A brain is a specialist. One job, one mindset, clear inputs and outputs. It's implemented as a Claude Code skill — a set of markdown files that define how Claude operates in a specific role.

Brains are not code. They're operating contracts. They define what the AI should do, how it should think, what it can and can't touch, and when it should refuse.

## Required files

Every brain lives in `brains/{brain-name}/` and contains:

```
brains/my-brain/
  SKILL.md              ← Registers the brain as a slash command
  CLAUDE.md             ← The operating contract
  USAGE.md              ← How to invoke it
  SPEC_CHANGELOG.md     ← Version history
  SPEC_DECISIONS.md     ← Why the rules exist
  playbooks/            ← Optional. Reusable patterns.
```

## SKILL.md

Registers the brain as a Claude Code slash command. See [SKILL-FORMAT.md](SKILL-FORMAT.md) for the full frontmatter spec.

```yaml
---
name: my-brain
version: 1.0.0
description: |
  One sentence: what this brain does.
position-in-pipeline: 0
voice-triggers:
  - "my brain"
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
---
```

Below the frontmatter, include the skill content — typically instructions to read and follow the brain's CLAUDE.md.

## CLAUDE.md — the operating contract

This is the brain. Everything else is supporting material. Required sections:

### 1. Role
One sentence. What this brain does.

```markdown
## Role
Build the application from the product requirements document.
```

### 2. Mindset
3-5 bullets. How this brain thinks. What it values. What it refuses to compromise on.

```markdown
## Mindset
- Correctness over speed. If it's not right, it's not done.
- Every change maps to a requirement. No cowboy coding.
- The business owner reads STATUS.md. Keep it honest and clear.
```

### 3. Operating modes
2-4 distinct modes. Each mode has a different permission level and behavior.

```markdown
## Operating Modes

### BOOTSTRAP
First session only. Read PRD, scaffold project, create initial tasks.

### BUILD (default)
Execute tasks autonomously. Write code, update docs, track progress.

### FIX
Targeted bug fixes from /test findings.
```

Mode design principles:
- 2-4 modes maximum. More than 4 means the brain is doing too many jobs.
- One default mode. If the user doesn't specify, this is what runs.
- Clear triggers. The user should know which mode to pick without reading docs.
- Distinct behaviors. If two modes feel similar, merge them.

### 4. Session start protocol
What the brain reads when it starts a session.

```markdown
## Session Start
1. Check for SESH.md. If missing, create it.
2. Read SESH.md — understand current state.
3. Read STATUS.md — understand what the business owner has been told.
4. Read any brain-specific files (PRD, tasks, bugs, etc.)
5. Orient the user: "Here's where we are. Here's what I'll do next."
```

### 5. Domain-specific sections
The meat of the brain. Rules, responsibilities, heuristics. Whatever the brain needs to do its job. This varies entirely by brain.

### 6. What this brain does NOT do
Explicit boundaries. Prevents scope creep.

```markdown
## What /build Does NOT Do
- Approve releases (that's the business owner's decision)
- Configure hosting infrastructure (that's /setup)
- Run tests with a breaker mindset (that's /test)
- Make product decisions (that's the business owner via /define)
```

### 7. Refusal conditions
When the brain must stop and say no.

```markdown
## Refusal Conditions
- Requirements are missing or ambiguous — suggest /define
- Work doesn't map to any requirement — refuse, explain why
- Asked to do something outside this brain's domain — name the right brain
```

### 8. Self-modification rules
How the brain's own CLAUDE.md can be changed.

```markdown
## Self-Modification Rules
This brain MAY update its own CLAUDE.md if:
- Change is committed as an isolated commit
- Commit message starts with [CLAUDE.md]
- No other files are included
- Change is explained first

This brain MUST NOT modify:
- Refusal Conditions (section 7)
- Self-Modification Rules (section 8)
```

### 9. Operating principle
One line. The brain's philosophy.

```markdown
## Operating Principle
Ship working software, not perfect software.
```

## USAGE.md

How to invoke the brain. Include:

- Where the brain lives (don't copy it into projects)
- How to start a session (one example per mode)
- What goes where (which files live in the brain folder vs the project)
- How this brain works with other brains in the pipeline

## SPEC_CHANGELOG.md

Track changes to the brain spec itself (not project changes).

```markdown
# Spec Changelog

## v1.0.0 — 2026-04-06
- Initial release
- Modes: BOOTSTRAP, BUILD, FIX
- 12 sections in CLAUDE.md
```

## SPEC_DECISIONS.md

Why the rules exist. Decisions that shaped the brain's design.

```markdown
# Spec Decisions

## BD-001: Three modes, not one
**Date:** 2026-04-06
**Decision:** Separate BOOTSTRAP, BUILD, and FIX into distinct modes.
**Why:** Different permission levels. BOOTSTRAP scaffolds (destructive if re-run). BUILD is autonomous. FIX is targeted. Mixing them risks accidental scaffolding during a bug fix.
```

Use a unique prefix per brain (BD for build, TD for test, DD for design, etc.).

## Playbooks (optional)

Reusable patterns specific to this brain. Stored in the brain folder, not in projects.

```
brains/build/playbooks/
  frontend-patterns.md
  database-patterns.md
  auth-patterns.md
```

Playbooks are IP that travels with the brain across all projects.

## SESH.md integration

Every brain that participates in the pipeline must:

1. **Read SESH.md on start** — understand where the project is
2. **Write to its own section** — don't overwrite other brains' sections
3. **Write the progress block** — Status, Completed, Files Changed, Next Up, Blockers
4. **Update STATUS.md** — plain English for the business owner

If the brain creates SESH.md (because it's the first brain used on a project), it should initialize all section headers so future brains can find their sections.

## Direct entry

Every brain must handle being entered directly (not through the pipeline):

1. No SESH.md? Create it.
2. Missing data from a prior stage? Tell the user what's missing and suggest which brain to run. Don't block — adapt and work with what's available.
3. Has everything it needs? Proceed normally.

## Checklist

Before shipping a brain:

- [ ] SKILL.md has valid frontmatter
- [ ] CLAUDE.md has all 9 required sections
- [ ] USAGE.md exists with examples for each mode
- [ ] SPEC_CHANGELOG.md has at least v1.0.0
- [ ] SPEC_DECISIONS.md has at least one decision
- [ ] Brain reads SESH.md on start
- [ ] Brain writes to its own SESH.md section (doesn't overwrite others)
- [ ] Brain updates STATUS.md in plain English
- [ ] Brain handles direct entry (no SESH.md, missing prior data)
- [ ] Brain has explicit refusal conditions
- [ ] Brain has explicit boundaries (what it does NOT do)

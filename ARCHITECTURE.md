# Architecture

How A Player Brains works under the hood.

## Overview

A Player Brains is a set of specialist AI brains, each implemented as a Claude Code skill (slash command). They share state through two files in the project directory and follow a linear pipeline from problem discovery to deployment.

```
/aplayerbrains → /discover → /plan → /setup → /define → /design → /build → /test → /launch
```

Three utility skills support the pipeline: /wrap (pause and resume), /status (where am I?), /upgrade (get latest brains).

## The two files

Every brain reads and writes two files in the project root:

### SESH.md (brain-to-brain contract)

Structured handoff data. Each brain owns a section. Sections accumulate as the project moves through the pipeline — brains add to SESH.md, they never overwrite other brains' sections.

```
## Problem          ← written by /discover
## Direction        ← written by /plan
## Infrastructure   ← written by /setup
## Requirements     ← written by /define
## Design           ← written by /design
## Build            ← written by /build
## Testing          ← written by /test
## Deployment       ← written by /launch
```

Every brain also writes a standard progress block at the bottom:

```
## Status: [DONE | CONTINUING | BLOCKED | ERROR]

### Completed This Session
### Files Changed
### Next Up
### Blockers
```

### STATUS.md (human-readable dashboard)

Plain English. The business owner reads this. Every brain updates it with what happened and what's next. No technical jargon. No code references.

Later pipeline stages add structured fields:
- Ship readiness: RED / YELLOW / GREEN (added by /test)
- Version and URL (added by /launch)

## How brains hand off

Each brain follows the same protocol:

**On start:**
1. Check if SESH.md exists
2. If yes: read it, understand current state, continue
3. If no: create it (the brain is the first touch on this project)
4. Read STATUS.md if it exists
5. Orient the user: "Here's where we are. Here's what I'll do."

**On finish (or /wrap):**
1. Update SESH.md — own section + progress block
2. Update STATUS.md — plain English summary
3. If wrapping: generate continuation prompt naming the next brain

## Direct entry

Any brain can be entered directly without going through the full pipeline. When a brain is entered directly:

1. It creates SESH.md if it doesn't exist
2. It checks whether it has what it needs from prior stages
3. If something is missing, it tells the user: "I don't have a validated problem yet. You might want to run /discover first. Or tell me about the problem now and I'll work with what I have."
4. It does NOT block. It adapts.

This means the pipeline is the recommended path, but not the only path. Someone who just wants to test an existing app can type /test directly. Someone who just wants a design mockup can type /design directly.

## /wrap and re-entry

/wrap is the universal pause button. It:

1. Captures what was done this session
2. Updates SESH.md (Status: CONTINUING)
3. Updates STATUS.md
4. Generates a continuation prompt ready to paste into the next session

The continuation prompt includes:
- Which brain to re-enter
- What mode
- Where work stopped
- What's next

**Backward movement:** /wrap can point to a different brain than the one that just ran. If /test finds bugs, /wrap generates a continuation prompt pointing to /build FIX. After /build fixes them, /wrap points back to /test VERIFY. The pipeline stays linear — /wrap handles direction changes.

## SESH.md accumulation

Each brain owns its section and only writes to it. This prevents overwrites as the document travels the pipeline.

| Brain | Section | What it writes |
|-------|---------|----------------|
| /discover | `## Problem` | Validated problem statement — who has it, what they do today, why it hurts |
| /plan | `## Direction` | Top risks, pre-decided responses, guardrails, recommended approach |
| /setup | `## Infrastructure` | Platform choice, repo URL, branch mapping, deploy config location |
| /define | `## Requirements` | PRD location, scope summary (in/out), stage breakdown |
| /design | `## Design` | Design decisions, mockup/Figma locations, visual direction confirmed |
| /build | `## Build` | Architecture decisions, current task, progress, files changed |
| /test | `## Testing` | Coverage summary, bugs found, severity breakdown, ship readiness |
| /launch | `## Deployment` | Version, live URL, deploy log location, rollback command |

## Progress signaling

The standard progress block at the bottom of SESH.md uses structured markers that can be parsed programmatically:

**Status signal:**
```markdown
## Status: DONE
```
Valid values: `DONE`, `CONTINUING`, `BLOCKED`, `ERROR`

**Blocker signal:**
```markdown
### BLOCKED: [reason]
```

**Detection patterns (regex):**
```
Done:       /##\s*Status:\s*DONE/i
Continuing: /##\s*Status:\s*CONTINUING/i
Blocked:    /###?\s*BLOCKED:\s*(.+)/i
Error:      /##\s*Status:\s*ERROR/i
Completed:  /\[x\]\s*(TASK-\d+|BUG-\d+)/gi
```

See [PROGRESS-SIGNALING.md](PROGRESS-SIGNALING.md) for the full spec.

## Config system

User-level configuration lives at `~/.apb/config.yaml`. Created by /setup.

```yaml
github_user: "username"
platform: "render"           # render | vercel
default_branch: "main"
staging_branch: "staging"
```

Brains that need infrastructure config (/define, /design, /build, /launch) read from this file. Brains that run before /setup (/discover, /plan) don't need it.

Project-level deployment config lives at `deploy.json` in the project root. Also created by /setup.

```json
{
  "targets": {
    "staging": {
      "branch": "staging",
      "url": "https://staging.example.com"
    },
    "production": {
      "branch": "main",
      "url": "https://example.com",
      "confirm": true
    }
  }
}
```

## Composition

Brains can use other brains' thinking internally without exposing separate commands:

- /plan runs premortem, inversion, bottleneck analysis, and optionality mapping as part of its process. These are thinking tools embedded in /plan, not standalone commands.
- /aplayerbrains reads SESH.md and routes to the appropriate brain. It's a router, not a worker — it doesn't modify project state.
- /wrap reads the current brain's spec to list available modes in the continuation prompt.

## The front door: /aplayerbrains

The one command the business owner needs to remember.

**No SESH.md found:** "Looks like a new project. Let's start by finding the real problem." Routes to /discover.

**SESH.md exists:** Reads current state, determines pipeline stage, tells user where they are, suggests next brain.

**After /wrap:** Reads continuation state, offers to resume where they left off.

## Brain file structure

Every brain follows the same file structure (see [BRAIN-BLUEPRINT.md](BRAIN-BLUEPRINT.md) for full spec):

```
brains/{brain-name}/
  SKILL.md              ← Frontmatter + skill registration
  CLAUDE.md             ← Operating contract (the brain's rules)
  USAGE.md              ← How to invoke, modes, examples
  SPEC_CHANGELOG.md     ← Version history of the brain spec
  SPEC_DECISIONS.md     ← Why the rules exist
  playbooks/            ← Optional. Reusable patterns.
```

## Security

See [SECURITY.md](SECURITY.md) for how secrets, auth, and data privacy are handled.

## Skill file format

See [SKILL-FORMAT.md](SKILL-FORMAT.md) for the YAML frontmatter spec that registers brains as slash commands.

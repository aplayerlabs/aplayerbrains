# /wrap — Usage

## Where it lives

```
playbooks/wrap/
  SKILL.md
  CLAUDE.md
  USAGE.md
  SPEC_CHANGELOG.md
  SPEC_DECISIONS.md
```

Do not copy these files into your project. The skill system reads them from the playbooks directory.

## How to invoke

```
/wrap
```

Or say: "wrap up", "pause", "stop here"

## Modes

### WRAP (default)

Manual pause. You decide when to stop.

```
/wrap
```

The playbook will:
1. Inventory what you did this session
2. Update SESH.md with your progress
3. Update STATUS.md in plain English
4. Output a continuation prompt you can paste into your next session

### AUTO

Triggered automatically when context is running low. You don't invoke this directly — the active playbook triggers it when it detects context filling up.

Same behavior as WRAP, but opens with "Context is getting full. Saving our progress now." and skips waiting for your input.

## What you get

After /wrap runs, you'll see a continuation prompt block like this:

```
---
## CONTINUATION PROMPT (copy everything below this line)
---

Read @playbooks/build/CLAUDE.md, then work on @cc/clients/Advance/Dashboard/

Read SESH.md first. Status: CONTINUING.

**Mode:** BUILD

## Where We Left Off
Implementing date range picker in src/components/DateFilter.tsx.
Basic structure done, calendar popover working.
Still need: validation, preset ranges (last 7d, 30d, etc), wire to filter state.

## Next Up
- Finish TASK-012: validation + presets for DateFilter
- TASK-013: Wire DateFilter to dashboard query params

## Blockers
None

---
**Other modes available:**
BOOTSTRAP — First session only. Scaffold project from PRD.
FIX — Targeted bug fixes from /test findings.
```

Copy everything below the "CONTINUATION PROMPT" line and paste it into your next Claude Code session to pick up where you left off.

## How it works with the pipeline

/wrap works with ANY playbook. It reads which playbook is active from SESH.md, looks up that playbook's modes, and generates the right continuation prompt.

The continuation prompt can point to a different playbook than the one you were using:

- **/test found bugs?** Continuation points to `/build FIX`
- **/build fixed the bugs?** Continuation points to `/test VERIFY`
- **Playbook's work is done?** Continuation points to the next playbook in the pipeline

## What goes where

| File | Location | Written by /wrap |
|------|----------|-----------------|
| SESH.md | Project root | Yes — progress block |
| STATUS.md | Project root | Yes — plain English update |
| Continuation prompt | Conversation output | Yes — copy/paste into next session |

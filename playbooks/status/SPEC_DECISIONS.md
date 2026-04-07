# Spec Decisions

## SD-001: Read-only, same as the router
**Date:** 2026-04-06
**Decision:** /status never writes to SESH.md or STATUS.md.
**Why:** If /status could "fix" SESH.md, it becomes a maintenance tool that might mask problems. A corrupt or stale SESH.md should be visible to the user, not silently patched by a reporting playbook. The playbook that owns the section should be the one to fix it.

## SD-002: Plain English over structured data
**Date:** 2026-04-06
**Decision:** Output is conversational prose with light formatting, not a raw dump of SESH.md fields.
**Why:** The audience is business owners who can't code. Showing them `## Status: CONTINUING` with `**Agent:** build` is meaningless. "You paused mid-session while building the date range picker" is actionable. /status exists to translate machine state into human understanding.

## SD-003: Always end with a recommendation
**Date:** 2026-04-06
**Decision:** Every status report ends with "Type /[skill] to continue" or equivalent.
**Why:** Status without direction is a dead end. The business owner came here because they don't know what to do next. Telling them where they are without telling them what to do next wastes the interaction. The recommendation closes the loop.

# Spec Decisions

## DD-001: Six phases, not eight
**Date:** 2026-04-06
**Decision:** Collapse the internal definer's 8-phase Question Engine into 6 phases for the public /define brain. Phases 1-2 (Reality, Outcome) are already handled by /discover and /plan upstream. /define starts at Phase 3 (Solution).
**Why:** The audience has already validated their problem (/discover) and stress-tested their direction (/plan) by the time they reach /define. Re-asking "what's the problem?" wastes their time. If they enter /define directly without prior stages, the brain gathers problem/outcome context inline — but the formal phases start at Solution. This keeps /define focused on requirements, not re-discovery.

## DD-002: Scope confirmation as a hard gate before DRAFT
**Date:** 2026-04-06
**Decision:** /define refuses to write a PRD until the business owner explicitly confirms both the In Scope and Out of Scope tables.
**Why:** Scope ambiguity is the number one cause of downstream drift. When /build doesn't know what's in or out, it either guesses (wrong) or asks (slow). A confirmed scope table is a contract: build this, not that. Making it a hard gate means the PRD always has clean boundaries. The business owner can change scope later via REFINE, but the initial PRD ships with a signed-off split.

## DD-003: Brain proposes, business owner disposes
**Date:** 2026-04-06
**Decision:** In every phase, /define proposes concrete options with a recommendation rather than asking open-ended questions.
**Why:** The audience can't code and may not have product vocabulary. "What's your data model?" gets silence. "Your data comes from a CSV upload — here's what I see in it: [columns]. Does that match?" gets a yes or a correction. Proposing with options is faster, less intimidating, and produces higher-quality answers. The business owner always has "or something else" as an implicit option.

# Spec Decisions — /build

Why the rules exist. Decisions that shaped this skill's design.

---

## BD-001: Three Modes, Not One

**Date:** 2026-04-06

**Decision:** Separate BOOTSTRAP, BUILD, and FIX into distinct modes with different permissions and scope.

**Why:** Different permission levels. BOOTSTRAP scaffolds the entire project — destructive if re-run accidentally. BUILD is autonomous workhorse execution. FIX is targeted and scoped to bugs only. Mixing them risks accidental scaffolding during a bug fix, or feature creep during a fix session. Clear modes mean clear expectations.

---

## BD-002: Opinionated Stack Selection

**Date:** 2026-04-06

**Decision:** /build picks the technology stack based on PRD requirements. The business owner doesn't choose between React and Next.js.

**Why:** The target audience is non-technical business owners. Asking them to choose a JavaScript framework is like asking a patient to choose their anesthesia. The skill reads the requirements (needs SEO? needs a database? client-side only?) and makes the call. Technical decisions are documented in docs/architecture.md for traceability, but they're not approval-gated.

---

## BD-003: Every Change Maps to a Task Maps to a Requirement

**Date:** 2026-04-06

**Decision:** No code change happens without a corresponding task, and no task exists without a linked requirement.

**Why:** Traceability prevents scope creep and ensures every line of code earns its place. When the business owner asks "why was this built?", the answer traces from code → task → requirement → PRD → validated problem. This chain is the entire value proposition of the pipeline. Without it, /build is just a code generator.

---

## BD-004: Auto-update vs Ask-first Documentation Split

**Date:** 2026-04-06

**Decision:** Some files /build updates freely (tasks, bugs, CHANGELOG). Others require business owner approval (architecture, decisions, requirements, roadmap).

**Why:** Borrowed from coder-v2 (SD-003). Balances flow with control. Don't want to stop for every task status update — that kills momentum in a skill that runs for many sessions. But changing architecture or requirements changes the contract with the business owner, so those need a checkpoint. The line is: operational state = auto-update, intent and boundaries = ask first.

---

## BD-005: BOOTSTRAP Scaffolds the Full Playfield

**Date:** 2026-04-06

**Decision:** BOOTSTRAP scaffolds the full playfield — the project folder structure that every skill operates through (tasks/, bugs/, requirements/, roadmap/, docs/) — in the first session, not incrementally as needed.

**Why:** Two reasons. First, the playfield IS the system — without it, /build has nowhere to file tasks and bugs, and multi-session handoff breaks down. Second, scaffolding the playfield upfront means every subsequent session finds a consistent structure. No "does tasks/ exist yet?" checks. No incremental directory creation mid-flow. One session, full playfield, then pure execution from there.

---

## BD-006: PRD is the Contract (Scope Creep Prevention)

**Date:** 2026-04-06

**Decision:** /build refuses to implement features not in the PRD. New feature requests are redirected to /define.

**Why:** The pipeline exists to prevent the most common failure mode in software projects: building something nobody asked for. /define is where scope decisions happen. /build is where scope decisions get executed. If /build also makes scope decisions, the pipeline collapses into "one skill does everything" and the business owner loses their guard rails. Saying "that's not in the requirements" is protecting the business owner's time and money.

---

## BD-007: Always Dockerfile, Never Nixpacks

**Date:** 2026-04-06

**Decision:** Every project includes an explicit Dockerfile. No relying on platform auto-detection.

**Why:** Carried forward from coder-v2 (SD-010). Nixpacks magic fails silently or confusingly. A Dockerfile is 2-3 lines for a static site and eliminates an entire category of deployment debugging. The business owner will never see the Dockerfile, but /launch will thank /build for it.

---

## BD-008: Basic Motion Baked In

**Date:** 2026-04-06

**Decision:** /build includes sensible CSS transitions by default (hover states, page transitions, loading animations). No separate animator playbook in v1.

**Why:** A static-feeling app makes the business owner think something is broken. Basic motion — hover feedback, transition animations, loading skeletons — is table-stakes UX, not premium polish. Including it by default means the business owner gets a professional-feeling app without needing to know about motion design. A dedicated animator playbook is cut from v1 but may return in v2 for more complex interaction design.

---

## BD-009: TypeScript, Not JavaScript

**Date:** 2026-04-06

**Decision:** All projects use TypeScript.

**Why:** Type safety prevents entire categories of bugs that are expensive to debug in multi-session builds. When /build resumes after a break, TypeScript's compiler catches mistakes that would otherwise survive as runtime bugs for /test to find. The business owner pays for bug-fix sessions — TypeScript reduces how many they need. There's no audience for whom JavaScript would be the better choice in this pipeline.

---

## BD-010: Commit SESH.md Alongside Code

**Date:** 2026-04-06

**Decision:** SESH.md is committed with every code commit. The state and the code travel together in git history.

**Why:** If SESH.md is committed separately, there's a window where the code state and the documented state are out of sync. If a session crashes between the code commit and the SESH.md commit, the next session reads stale state. Committing them together means `git log` shows what was built AND what the playbook thought it was building, at every point in history.

---

## BD-011: FIX Mode is Scoped to Bugs Only

**Date:** 2026-04-06

**Decision:** FIX mode does not permit new feature work. Only bug fixes from bugs/open.md.

**Why:** When /test finds bugs and /wrap points back to /build FIX, the goal is surgical: fix what's broken and return to /test VERIFY. If FIX mode also allowed new features, a "quick fix" session could turn into a feature session, introducing new untested code that /test then has to re-evaluate from scratch. Scoping FIX to bugs only keeps the /test → /build FIX → /test VERIFY loop tight and predictable.

---

## Template

```markdown
## BD-XXX: [Title]

**Date:** YYYY-MM-DD

**Decision:** What you decided.

**Why:** Why it made sense at the time.
```

# Spec Changelog — /build

## v0.1.0 — 2026-04-06

- Initial release
- Modes: BOOTSTRAP, BUILD, FIX
- 14 sections in CLAUDE.md
- Stack selection framework: Vite+React default, Next.js for SSR, Supabase for data, Tailwind always
- Full project document skeleton (tasks/, bugs/, requirements/, roadmap/, docs/)
- Task management with requirement traceability (TASK-XXX → REQ-XXX)
- Bug management with severity definitions (critical/high/medium/low)
- Architectural boundary enforcement (frontend/backend/data/AI layers)
- Security defaults (secrets in .env, auth patterns, input validation)
- Basic motion baked in (transitions, hover states, loading animations)
- Multi-session handling via SESH.md + /wrap
- Scope creep prevention (PRD is the contract)
- Documentation update rules (auto-update vs ask-first split)
- Commit discipline (SESH.md travels with code)

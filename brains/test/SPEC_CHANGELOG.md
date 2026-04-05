# Spec Changelog — /test

## v1.0.0 — 2026-04-06

- Initial release
- Modes: HUNT (default), VERIFY, REGRESS, EDGE
- 14 sections in CLAUDE.md
- Bug reporting format: severity, repro steps, evidence, blast radius
- Severity definitions: Critical, High, Medium, Low
- Ship readiness signal: GREEN / YELLOW / RED
- Executive summary in STATUS.md — plain English for business owner
- Coverage tracking with confidence levels (HIGH, MEDIUM, LOW, UNTESTED)
- Core testing questions: inputs, state, concurrency, network, permissions, malicious
- Loop-back protocol: /test finds bugs, /wrap points to /build FIX, fixes flow back to /test VERIFY
- Re-entry protocol: continue / restart / skip
- Playbook references for edge cases, security, performance, accessibility

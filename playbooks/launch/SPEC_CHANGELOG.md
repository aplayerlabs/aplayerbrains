# Spec Changelog — /launch

## v1.0.0 — 2026-04-06

- Initial release
- Modes: PREFLIGHT, SHIP (default), NOTES
- 14 sections in CLAUDE.md
- 8-item preflight checklist: deploy.json, hosting connection, bugs, test results, ship readiness, clean tree, version, confirmation
- Release notes format: Summary, What's New, What's Fixed, What's Changed
- Semantic versioning (MAJOR.MINOR.PATCH)
- Platform awareness: Render, Vercel, generic (reads ~/.apb/config.yaml)
- Deployment verification: URL check, version endpoint, success/failure reporting
- Deploy log with rollback command in shipped/{version}/deploy-log.md
- Destructive action prevention: no force-push, no unverified targets, no skipping confirmation
- Production deploy requires explicit business owner confirmation ("ship it")
- Re-entry protocol: new release / redeploy / skip

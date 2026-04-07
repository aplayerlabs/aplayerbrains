# Spec Decisions

## SD-001: Two modes — INFRA and PROJECT
**Date:** 2026-04-06
**Decision:** Separate first-time-ever infrastructure setup (INFRA) from per-project deployment config (PROJECT).
**Why:** INFRA is a one-time event — creating accounts, learning the secrets pattern, saving global config. PROJECT happens for every new app. Mixing them means returning users wade through account creation prompts they don't need. INFRA auto-triggers when `~/.apb/config.yaml` is missing; PROJECT is the default when it exists.

## SD-002: Render as the opinionated default
**Date:** 2026-04-06
**Decision:** Recommend Render over Vercel, Netlify, Fly.io, or Railway.
**Why:** The audience can't code. Render has the simplest mental model: push to a branch, your app goes live. Free tier is generous (750 hours/month). Git-push deploys mean no CLI tools or manual build steps. Vercel is supported as an alternative for purely static sites, but Render is the first recommendation because it handles both static and server-rendered apps with the same workflow.

## SD-003: External steps as guided instructions, not automation
**Date:** 2026-04-06
**Decision:** /setup tells the business owner what to click and where, rather than automating account creation or API calls.
**Why:** Account creation requires human identity (email verification, passwords, billing). Automating it would mean storing credentials we shouldn't hold, impersonating the user, and creating accounts they don't control. The playbook guides; the human acts. This also teaches them where their infrastructure lives — they'll need to know when they log into Render or GitHub later.

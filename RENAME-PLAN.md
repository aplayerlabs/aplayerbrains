# Rename Plan: A Player Brains → A Player Playbooks

## Decisions made

- Front door command: `/playbooks`
- Repo name: `aplayerlabs/aplayerplaybooks` (confirm with Rossco)
- Install path: `~/.claude/skills/playbooks`
- Folder: `brains/` → `playbooks/`
- File: `BRAIN-BLUEPRINT.md` → `PLAYBOOK-BLUEPRINT.md`
- All "brain" → "playbook", "brain chain" → "playbook chain"

## Scope

- 675 occurrences across 58 files
- 2 folder renames (brains/ → playbooks/, brains/aplayerbrains/ → playbooks/playbooks/)
- 1 file rename (BRAIN-BLUEPRINT.md → PLAYBOOK-BLUEPRINT.md)
- GitHub repo rename
- Setup script rewrite

## Find/replace patterns (IN THIS ORDER — order matters for clean replacement)

1. `A Player Brains` → `A Player Playbooks`
2. `brain chain` → `playbook chain`
3. `Brain Chain` → `Playbook Chain`
4. `BRAIN CHAIN` → `PLAYBOOK CHAIN`
5. `brain-to-brain` → `playbook-to-playbook`
6. `BRAIN-BLUEPRINT` → `PLAYBOOK-BLUEPRINT`
7. `Brain Blueprint` → `Playbook Blueprint`
8. `brain blueprint` → `playbook blueprint`
9. `/aplayerbrains` → `/playbooks`
10. `aplayerbrains` (as folder/path reference, NOT GitHub URL) → `playbooks`
11. `brains/` (folder path) → `playbooks/`
12. `brain` → `playbook` (standalone word — careful not to replace inside other words)
13. `Brain` → `Playbook` (capitalized standalone)
14. `Brains` → `Playbooks` (plural capitalized, but NOT when part of "A Player Brains" which is already handled)

## CRITICAL: Do NOT replace

- GitHub URLs: `github.com/aplayerlabs/aplayerbrains` — repo rename happens separately on GitHub
- The word "brainstorm" or any compound word where "brain" is a substring of another word
- Inside node_modules/
- Inside .git/

## Folder renames (do BEFORE text replacement)

```bash
cd /Users/rosscopaddison/cc/apb/aplayerbrains
mv brains/aplayerbrains brains/playbooks
mv brains playbooks
mv BRAIN-BLUEPRINT.md PLAYBOOK-BLUEPRINT.md
```

## File-by-file manifest

### Root docs (12 files to edit)
- README.md (18 occurrences)
- ETHOS.md (11)
- ARCHITECTURE.md (46)
- PLAYBOOK-BLUEPRINT.md (65) ← after rename
- CONTRIBUTING.md (11)
- GETTING-STARTED.md (16)
- PLAN.md (77)
- PROGRESS-SIGNALING.md (9)
- ROADMAP.md (12)
- SECURITY.md (3)
- SKILL-FORMAT.md (13)
- SIMULATION-BRIEF.md (26)

### Infrastructure (3 files)
- setup (27 occurrences)
- .github/pull_request_template.md (2)
- project-template/STATUS.md (1)

### Per-playbook specs (42 files across 12 playbooks)
Every playbook folder has CLAUDE.md + USAGE.md + SPEC_DECISIONS.md (+ SKILL.md and SPEC_CHANGELOG.md for some):

| Playbook (new folder name) | CLAUDE.md | USAGE.md | SPEC_DECISIONS | SKILL.md | CHANGELOG | Total |
|---|---|---|---|---|---|---|
| playbooks (front door) | 30 | 7 | 4 | 3 | — | 44 |
| discover | 12 | 8 | 2 | — | 1 | 23 |
| plan | 10 | 6 | — | — | — | 16 |
| setup | 14 | 2 | 1 | 1 | — | 18 |
| define | 9 | 2 | 3 | — | — | 14 |
| design | 12 | 3 | 2 | — | — | 17 |
| build | 12 | 5 | 7 | — | — | 24 |
| test | 6 | 4 | 4 | — | — | 14 |
| launch | 12 | 5 | 3 | — | — | 20 |
| wrap | 44 | 8 | 5 | — | 1 | 58 |
| status | 22 | 5 | 2 | 1 | — | 30 |
| upgrade | 40 | 10 | 3 | 2 | 2 | 57 |

## Execution order

1. Rename folders and file (mv commands)
2. Run find/replace across all files (patterns 1-14 in order)
3. Update setup script paths
4. Update all internal cross-references (SKILL.md body text referencing CLAUDE.md paths)
5. Verify build/lint (no broken references)
6. Rename GitHub repo: aplayerlabs/aplayerbrains → aplayerlabs/aplayerplaybooks
7. Update git remote
8. Update GitHub URLs in files that reference the repo
9. Push
10. Re-run setup script to re-register slash commands
11. Update memory files and website references

## Continuation prompt for fresh session

```
Read /Users/rosscopaddison/cc/apb/aplayerbrains/RENAME-PLAN.md and execute it.

The repo is at /Users/rosscopaddison/cc/apb/aplayerbrains/. Rename everything from "brain/brains" to "playbook/playbooks" following the plan exactly. The front door command becomes /playbooks.

Do the folder/file renames first, then run the find/replace patterns in order, then verify nothing is broken. Do NOT rename the GitHub repo — I'll do that manually. But DO update the git remote URL after I confirm the new repo name.
```

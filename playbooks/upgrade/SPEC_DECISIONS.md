# Spec Decisions

## UD-001: All-or-nothing upgrades
**Date:** 2026-04-06
**Decision:** /upgrade pulls all playbooks at once. No selective per-playbook upgrades.
**Why:** Playbooks depend on shared contracts (SESH.md format, STATUS.md format, progress signaling). Upgrading one playbook but not others risks version mismatches where playbook A writes a field that playbook B doesn't know how to read. All-or-nothing keeps the system coherent.

## UD-002: Default to cancel on local modifications
**Date:** 2026-04-06
**Decision:** When local modifications are detected, the default action is cancel, not upgrade.
**Why:** If someone has customized a playbook (added heuristics, tweaked modes, adjusted thresholds), that's intentional work. Silently overwriting it is destructive. The safe default is to preserve their changes and let them explicitly choose to overwrite.

## UD-003: CHECK mode exists as a separate mode
**Date:** 2026-04-06
**Decision:** Dry-run checking is a distinct mode, not a flag on the upgrade command.
**Why:** "What's new" is a different intent than "upgrade now." Making it a mode means the user can ask "any updates?" without worrying about accidentally triggering an upgrade. Low friction for curiosity, explicit action for changes.

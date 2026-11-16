# Issue

**Title:** feat(store): path-based install layout + local-skill awareness + uninstall

## Description

Part of the in-app Pantheon Store hierarchy/install work (agent side).

## What
- **installer.py** — install skills under their original hierarchical source path (`skills/<path>/SKILL.md`) instead of a flat prefixed dir; `uninstall()` gained a `path` param so it cleans up that layout.
- **room.py** — `get_local_skills` now also reports factory-bundled sub-skills (nested resource `.md` files like `live_view/cytoscape/cytoscape.md`) so the store UI shows them as built-in (already shipped), not installable; new `uninstall_store_package` tool; install records + uses the original `path` in the local install manifest; installed-check is path-aware.
- **seed.py** — thread the original source path end-to-end (factory + external discovery → manifest → `_publish_one`) so each package carries an accurate `path`; backfills it on content-unchanged re-seeds (so reviews are preserved, no re-review tokens).

## Test
- Re-ran the seed locally against the dev hub: 2105 updated / 9 new / 0 failed, reviews preserved (2102), 2107/2107 skills with accurate paths.
- Verified in the local UI: built-in detection, path-restore install, subtree install, cascade uninstall.

Pairs with pantheon-hub (package `path` + descendants endpoint) and pantheon-ui (Installed hierarchy + detail).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3edea786b42d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
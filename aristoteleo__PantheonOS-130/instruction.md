# Issue

**Title:** feat(skills): per-deployment skill denylist (PANTHEON_EXCLUDED_SKILLS)

## Description

## What
Adds a per-deployment skill denylist to the learning system. `SkillStore` accepts `excluded_skills`; excluded skills are filtered out of `scan_headers` (so they never reach the injected skill index) and refused by `load_skill` (so a stale/guessed name can't pull the content back in). `LearningRuntime` reads the comma-separated `PANTHEON_EXCLUDED_SKILLS` env var and threads it through.

## Why
A host app whose own agent already reaches that app's data via a dedicated MCP (e.g. Virtual Embryo → `ve_curator`) shouldn't ALSO see the packaged factory skill for that app — the agent ends up flip-flopping between the MCP and the skill's raw-HTTP path. This hides the skill *in that sandbox only*; it stays in the factory tree for every other PantheonOS agent. Parallels the existing per-app `mcp.json` server disable.

The denylist is applied at the `SkillStore` discovery choke point (not at materialization) because the store scans the packaged factory skills dir directly — so skipping materialization alone would not hide the skill.

## Pairs with
pantheon-hub PR that sets `PANTHEON_EXCLUDED_SKILLS=virtualembryo` for the VE app. Inert + harmless until both land.

## Verified (locally)
- **Unit:** against the real factory skills, denylist `["virtualembryo"]` hides exactly that skill, preserves the other 8 (incl `live_view`), and `load_skill("virtualembryo")` returns `None`.
- **Full path:** `LearningRuntime.initialize` → `SkillStore` → `SkillInjector.build_skill_index()` drops `virtualembryo` from the injected index while keeping the rest.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fd562d6e524`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
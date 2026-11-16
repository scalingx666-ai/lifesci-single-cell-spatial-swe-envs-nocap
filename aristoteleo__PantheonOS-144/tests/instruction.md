# Issue

**Title:** fix(store): repair claude-scientific (0→149) + add DeepMind science-skills (+34)

## Description

## Key finding
`claude-scientific` (K-Dense) was silently contributing **0 skills** — the upstream repo moved skills from `scientific-skills/` → `skills/`, but our `skills_dir` still pointed at the old empty dir (confirmed 0 packages on staging). One-line fix recovers **149** skills.

## Changes
- **Fix `claude-scientific`**: `skills_dir` `scientific-skills` → `skills` → +149.
- **Add `science-skills`** (google-deepmind, Apache-2.0/CC-BY): 37 SKILL.md (AlphaGenome/AlphaFold/UniProt/ClinVar + 30 DBs). New optional per-source `exclude` drops 3 non-science infra skills (uv, scienceskillscommon, workflow_skill_creator) → **34**.
- New reusable `exclude` mechanism in `_discover_external_skills`.

Net **+183**. Verified locally: claude-scientific now discovers 149, science-skills 34 (meta excluded); `py_compile` clean.

Notes: anthropic/life-sciences skipped (6 skills, mostly MCP marketplace). Kept DeepMind's DB-access skills (may be higher quality than existing equivalents; /recommend ranks by reviewer quality) — `exclude` is extendable if specific drops are wanted. Cross-source topical duplication is a known separate curation problem.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46b42dc8e3cd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
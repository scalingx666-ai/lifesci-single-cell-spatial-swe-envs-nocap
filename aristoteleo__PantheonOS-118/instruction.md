# Issue

**Title:** store: bioSkills/SciAgent sources + references, auto-versioning, dep-install, dedup

## Description

Store-side enhancements to the seed + CLI (`pantheon/store/{seed,cli,client}.py`).

## What
| Area | Change |
|---|---|
| **External sources** | Add **bioSkills** (GPTomics, MIT, ~537 skills) and **SciAgent-Skills** (jaechang-hits, CC-BY, ~197) to `EXTERNAL_REPOS` |
| **Skill references** | Extract cross-references at ingest (relative `[x](./a/SKILL.md)` links + `## Related Skills` name lists), resolve to exact store names, thread through publish |
| **Dependency install** | `pantheon store install <pkg>` now installs the reference closure (root + referenced skills); `--deps=False` / `--nodeps` to opt out |
| **Auto-versioning** | Re-seeding an existing package publishes a **new patch version when content changed** (was a no-op skip) → real content sync + version history |
| **Collision handling** | Two different skills with the same `name:` frontmatter (e.g. OpenClaw `pptx` + `pptx-official`): exact dups dropped, same-name-different skills disambiguated (`..._pptx`, `..._pptx-2`) so each keeps a distinct id |

## Verification (local hub)
- Seed: bioSkills 537 + SciAgent 197 ingested; 398 packages carry references (1416 edges).
- Re-seed unchanged → 0 published / 0 updated / all skipped. Changed → new `1.0.x` version.
- `install omics_group` → root + 44 referenced skills. Collisions → 0 remaining duplicate names; `pptx-official` preserved as a distinct id.

Companion PRs: pantheon-hub (references/graph/version API), pantheon-ui (store UI + relationship graph).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f87587c1b66`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
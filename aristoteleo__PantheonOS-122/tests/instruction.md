# Issue

**Title:** store: references, content-sync auto-versioning, dependency install, name dedup

## Description

Store seed/CLI enhancements, on top of #118 (bioSkills/SciAgent sources). Pairs with pantheon-hub#16 + pantheon-ui#9.

## What
| Area | Change |
|---|---|
| **Skill references** | Extract cross-refs at ingest (relative `[x](./a/SKILL.md)` links + `## Related Skills` name lists), resolve to exact store names, thread through publish |
| **Dependency install** | `pantheon store install <pkg>` installs the reference closure (root + referenced skills); `--deps=False`/`--nodeps` to opt out |
| **Auto-versioning** | Re-seeding an existing package publishes a **new patch version when content changed** (was a no-op skip) → real content sync + version history |
| **Name dedup** | Two different skills with the same `name:` frontmatter (e.g. OpenClaw `pptx` + `pptx-official`): exact dups dropped, same-name-different skills disambiguated (`..._pptx`, `..._pptx-2`) → distinct ids |
| **client** | `publish_version` 409 treated as a skip (idempotent re-seed) |

## Verified (local hub)
- 398 packages carry references (1416 edges); `install omics_group` → root + 44 deps.
- Re-seed unchanged → 0 published / 0 updated / all skipped; changed → new `1.0.x`.
- Collisions → 0 remaining duplicate names; `pptx-official` preserved as a distinct id.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f5cceaa7e92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
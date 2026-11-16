# Issue

**Title:** ci(audit): add ttf-parser to unmaintained-ignore list (closes #331 + stale #332)

## Description

Closes the two RUSTSEC-triggered issues auto-filed by \`rustsec/audit-check\` on 2026-07-06.

## #331 — \`ttf-parser\` unmaintained (RUSTSEC-2026-0192)

Adds \`RUSTSEC-2026-0192\` to the \`rustsec/audit-check\` ignore list in \`ci.yml\`, matching the existing \`RUSTSEC-2024-0436\` (\`paste\` unmaintained) pattern.

Rationale: \`ttf-parser 0.25.1\` is transitive five levels deep — \`trim-galore → fastqc-rust → resvg → usvg → fontdb → ttf-parser\` (also via \`rustybuzz\`). The advisory recommends migrating to \`skrifa\` (Google Fonts' \`fontations\` project). Nothing we can fix at this level — the migration has to happen upstream at \`resvg\` or \`fastqc-rust\`. Matches the existing policy: **suppress only \`unmaintained\` warnings where the fix has to land in an upstream crate; CVE-class advisories remain loud.**

## #332 — \`anyhow\` unsoundness — already resolved

Not addressed in this PR because it was already patched: \`anyhow 1.0.102 → 1.0.103\` (fixes RUSTSEC-2026-0190 in \`Error::downcast_mut()\`) landed in \`cd34afc\` (PR #319, cargo-patch-minor group) **before** the audit-check action even filed the issue.

The action opens GitHub issues when it detects advisories but doesn't close them when advisories are resolved upstream. Closing #332 by hand after this PR merges with a pointer to \`cd34afc\` for the audit trail.

Additional safety check: our source has zero \`downcast_mut\` or \`.downcast(\` calls anywhere in \`src/\`, so the unsound code path was unreachable in our binary even at 1.0.102.

## Test plan

- [x] YAML syntax check (block-scalar \`|\` format is what \`rustsec/audit-check\` expects for multiple ignores)
- [ ] CI Security audit passes on this PR (no regressions from the ignore-list expansion)
- [ ] Post-merge: close #331 and #332 with commit-anchored comments (dev ≠ default branch, keyword-based auto-close doesn't fire — memory: \`feedback_auto_close_keyword\`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0fdbafe5831`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
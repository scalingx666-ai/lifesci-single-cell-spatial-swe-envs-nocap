# Issue

**Title:** ci(audit): add rustybuzz to unmaintained-ignore list

## Description

(RUSTSEC-2026-0206 — \`rustybuzz\` unmaintained, filed by \`rustsec/audit-check\` on 2026-07-13).

## Rationale

Adds \`RUSTSEC-2026-0206\` to the \`rustsec/audit-check\` ignore list, alongside the existing \`RUSTSEC-2024-0436\` (\`paste\`) and \`RUSTSEC-2026-0192\` (\`ttf-parser\`) entries.

\`rustybuzz 0.20.1\` is transitive four levels deep — \`trim-galore → fastqc-rust → resvg → usvg → rustybuzz\` — sitting alongside \`ttf-parser\` under the same resvg/usvg font-and-text stack. The \`harfbuzz\` team announced end-of-maintenance on the pure-Rust port. Nothing we can fix at this level; needs upstream migration at resvg or fastqc-rust to a maintained text-shaping crate.

Matches the existing policy: **suppress only \`unmaintained\` warnings where the fix has to land in an upstream crate; CVE-class advisories remain loud.**

## The pattern

This is the third RUSTSEC \`unmaintained\` advisory to fire off the same resvg/usvg subtree in a short window — first ttf-parser (yesterday's #331), now rustybuzz. Worth noting as a signal that this subtree's maintenance risk is growing, but no action beyond the ignore list makes sense until either fastqc-rust or resvg upstream ships a maintained replacement.

## Test plan

- [x] YAML format matches yesterday's successful #342 (comma-separated per \`rustsec/audit-check\`'s input schema)
- [ ] Security audit passes on this PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `944af72ec7ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
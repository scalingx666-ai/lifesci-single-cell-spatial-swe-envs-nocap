# Issue

**Title:** chore(dependabot): ignore noodles (exact-pinned for byte-identity)

## Description

Closes the review loop on #326.

## Why

\`noodles\` is exact-pinned to \`=0.88.0\` in \`Cargo.toml\` for byte-identity of the uBAM I/O path. The crate's pre-1.0 (0.x) semver doesn't guarantee wire-format or API stability across minor bumps, and any real noodles migration would need scoped human review coordinated with Bismark's cross-tool byte-identity CI (per \`src/bam.rs\` + Bismark's own pin).

Dependabot proposed \`0.88.0 → 0.109.0\` in #326 despite the exact-pin (Dependabot ignores pin operators when proposing bumps). Result: 5 failed CI checks (Rust Tests × 2, Reproducibility, Lint, Coverage — all compile/API errors), \`Validate vs Perl TrimGalore\` and \`Validate uBAM input\` skipped as downstream. The pin is doing its job; Dependabot's weekly re-proposal isn't.

## Change

Adds an \`ignore\` entry to the cargo ecosystem block:

\`\`\`yaml
ignore:
  - dependency-name: "noodles"
\`\`\`

All other cargo deps continue to flow through the \`cargo-patch-minor\` group as before.

## Test plan

- [x] YAML parses (git diff looks clean, indentation matches surrounding block)
- [ ] Next Monday's Dependabot run does not re-propose \`noodles\` (observational — no immediate CI signal since dependabot.yml is only exercised by scheduled runs)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e629919147f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
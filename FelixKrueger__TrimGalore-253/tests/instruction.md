# Issue

**Title:** chore: clear deferred CI + test items (#246 §5.2, #247 #2/#3/#4/#7)

## Description

## Summary

Sweeps the previously-deferred items from #246 / #247 into a single bundle. All additive, none touch the trimming hot path.

## Items in this PR

| | What | Source |
|---|---|---|
| 1 | macOS matrix on \`rust-tests\` (\`ubuntu-latest\` + \`macos-latest\`) | **#247 #2** |
| 2 | \`Run tests (release)\` step (LTO catch) | **#247 #3** |
| 3 | \`coverage\` CI job via \`cargo-llvm-cov\` (LCOV artifact, 14-day retention) | **#247 #4** |
| 4 | \`justfile\` for local CI parity (\`fmt\`, \`clippy\`, \`test\`, \`test-release\`, \`ci\`, \`reproduce\`, \`validate-paired-end\`, \`logos\`, \`docs\`, \`docs-dev\`) | **#247 #7** |
| 5 | First unit test in \`src/parallel.rs\`: parallel/serial \`TrimStats\` parity | **#246 §5.2** |

\`TrimStats\` gained a \`PartialEq\` derive so a single \`assert_eq!\` covers every field — future fields are automatically covered without test edits.

## Deliberately NOT here

- **#247 #8** (\`cargo-nextest\`) — process-isolation swap is non-trivial. Several existing tests share \`std::env::temp_dir().join(...)\` paths that could collide under nextest's per-process model. Wants its own focused audit.
- **#246 comprehensive \`parallel.rs\` coverage** — naturally iterative; the §5.2 parity test is a meaningful start.
- **#246 bonus** (upstream Dongze's proptest harness) — needs his code.
- **#248 #4** (Myers' alignment) — needs his ephemeral branch (gone).
- **#245 B** (poly-A alignment divergence) — investigation, not fix.

## Test plan

- [x] \`cargo test --release\` — 180 passed (179 + 1 new)
- [x] \`cargo fmt --all -- --check\` — clean
- [x] \`cargo clippy --all-targets --release -- -D warnings\` — clean
- [x] YAML \`ci.yml\` parses
- [ ] CI on this PR exercises the new matrix entry (\`Rust Tests (macos-latest)\`), the new \`coverage\` job, and the new release-profile test step
- [ ] Coverage artifact downloadable from the run UI after merge

Addresses #246, #247.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f02d5d79e656`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
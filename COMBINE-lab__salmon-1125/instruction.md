# Issue

**Title:** chore(deps): drop the unused scc dependency

## Description

`scc` is declared in `crates/salmon-eqclass/Cargo.toml` and in the workspace dependency table, but nothing imports it: the concurrent builder is backed by `dashmap::DashMap`.

Removing it drops `scc` and its `sdd` dependency from the build graph. No behaviour change; `cargo test --workspace` is green.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d19bb9cdeb4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
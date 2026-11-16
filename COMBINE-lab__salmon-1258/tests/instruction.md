# Issue

**Title:** Follow-ups after 2.9.1: read-error context, --online wording, working release dry-run

## Description

## Follow-ups after 2.9.1

Three small changes, none of which affects quantification results.

### 1. Read errors: don't list candidate files when the error already names the culprit
When mapping fails while reading input, salmon adds the list of read files as context, because the FASTX parser doesn't say which file failed. piscem-rs is gaining a change that names the file in decoder errors (a truncated or corrupt compressed input), with a plain-language cause. That change is not yet released; it will be piscem-rs 0.12.2. When the error already names a file, the candidate list is now dropped. Parse errors, which still arrive without a path, keep it.

With the piscem-rs change, a truncated R2 now reports:
```
Error: deterministic mapping pass failed

Caused by:
    mapping failed: Error reading from buffer: trunc_2.fq.gz: compressed data ended early (the file is probably truncated: an incomplete download or copy?)
```
Before, the same failure gave "compressed data ended early", without naming the file at one thread and with a list of both read files at eight. On its own this change makes no difference, since today's errors don't contain a path.

### 2. `--online`: stop promising removal "in 2.7.0"
The help text, both warnings, the `--deterministic` no-op note, the CLI reference and the RAD/determinism guide still said removal was planned for 2.7.0. They now say it will be removed in a future release. Whether and when to actually remove the path is a separate decision.

### 3. `scripts/bump_and_publish.sh --dry-run` now validates the packages
`--dry-run` claimed to run `cargo publish --dry-run` per crate. But every command went through `run`, which only prints in dry-run mode, so it validated nothing.
- It now applies the same version bump in a scratch git worktree of `HEAD`, and runs `cargo publish --workspace --dry-run` there.
- That packages and verifies every crate at the new version, in dependency order. Cargo (≥ 1.90) supplies the not-yet-published `salmon-*` versions from a temporary local registry.
- The checkout is untouched and the scratch worktree is removed on exit. The real release path is unchanged.

Checked with `./scripts/bump_and_publish.sh 2.9.2 --publish --dry-run`: all 10 crates verified at 2.9.2. The script left no changes and no tag, and removed the worktree.

### Testing
`cargo test --release -p salmon-cli --locked`: 49 passed. fmt and clippy (`-D warnings`) on the touched crates are clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5e6b278c9ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** chore(deps): bump memmap2 0.9.10 → 0.9.11 (RUSTSEC-2026-0186)

## Description

## Summary

Single-line transitive-dep bump to clear [RUSTSEC-2026-0186](https://rustsec.org/advisories/RUSTSEC-2026-0186.html) (unchecked pointer offset in `memmap2 0.9.10`'s `advise_range` / `flush_range` functions). Fix released in `memmap2 0.9.11`.

**Dep chain:** \`memmap2 ← fontdb ← usvg ← resvg ← fastqc-rust 1.0.1 ← trim-galore\` — used for FastQC's SVG plot rendering. The exact-pinned \`fastqc-rust = "=1.0.1"\` upstream pin is preserved.

**Practical risk for TrimGalore:** ~zero. The vulnerable functions take attacker-controlled \`offset\`/\`len\` parameters, but no such input flows through TrimGalore's FastQC SVG render path (fonts are bundled/system, not user-supplied). Still worth fixing: clears the \`audit\` CI job red state surfaced by the auto-opened issue #324.

## Diff

\`Cargo.lock\` only — single version-line change for \`memmap2 0.9.10 → 0.9.11\`. No \`Cargo.toml\` change required (the version constraint is a transitive \`^0.9\` floor; the patch update resolves naturally).

## Test plan

- [x] \`cargo build --release\` clean
- [x] \`cargo test --release\` — 353 tests pass (unchanged from v2.3.0)
- [x] \`cargo fmt --all -- --check\` clean
- [x] \`cargo clippy --release --all-targets -- -D warnings\` clean
- [ ] CI \`audit\` job goes green (previously red on this advisory)
- [ ] All other CI lanes stay green (FASTQ byte-identity vs Perl 0.6.11, etc.)

 (will manually close after merge since the auto-close keyword only fires on default-branch merge per [`feedback_auto_close_keyword`](https://github.com/FelixKrueger/TrimGalore/blob/dev/CLAUDE.md))

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6528e54512e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
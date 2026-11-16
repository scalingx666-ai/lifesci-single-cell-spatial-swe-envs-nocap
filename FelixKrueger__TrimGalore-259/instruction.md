# Issue

**Title:** chore(release): v2.1.0-beta.7 + benchmark driver

## Description

## v2.1.0-beta.7

Single substantive change since beta.6: **Myers' bit-parallel adapter alignment prefilter** (,  item 4). Wraps an O(n) bit-vector pass in front of the existing scalar DP; conservative by design (only short-circuits when no match can possibly exist), preserving byte-identity by construction. @an-altosian measured this at −13.6% wall at cores=8 on his Buckberry prototype. Co-authored with him.

Three doc-only PRs also since beta.6: poly-A divergence migration note (#257, closing out #245), GHCR tag prefix correction (#256), install.md squash-followup (#255).

## scripts/benchmark.sh

New reproducible perf-benchmark driver for the Buckberry-scale comparison:

| Configuration | Cores | Tooling |
|---|---|---|
| Perl Trim Galore 0.6.11 + Cutadapt 5.2 | 1, 4, 8, 16 | igzip + pigz |
| Rust v2.1.0-beta.5 (pre-Buckberry-audit) | 1, 4, 8, 16, 24 | zlib-rs + gzp |
| Rust v2.1.0-beta.7 (post-Myers' prefilter) | 1, 4, 8, 16, 24 | zlib-rs + gzp |

`hyperfine --warmup 1 --runs 10` per condition, `--export-json` for downstream plotting, filesystem cache warmed once up front, beta.5-vs-beta.7 byte-identity cross-check on cores=8 output as a paranoia gate.

Designed for the Altos `oxy` EKS instance; all paths/cores/runs overridable via env vars. Full-matrix wall-time at Buckberry scale (84M PE reads): ~13 h. Run under tmux/nohup.

## Test plan

- [x] \`cargo build --release\` reports \`trim_galore 2.1.0-beta.7 (Oxidized Edition)\`
- [x] Tests still pass on this branch (188, unchanged from optimus_prime tip)
- [x] No stale beta.6 forward-pin references left (historical mentions in CHANGELOG / code comments preserved)
- [x] \`bash -n scripts/benchmark.sh\` parses clean
- [ ] Post-merge: \`gh workflow run release.yml --ref optimus_prime\` to actually publish
- [ ] Post-release: run \`scripts/benchmark.sh\` on \`oxy\` against Buckberry SRR24827373

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef2dce35101d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
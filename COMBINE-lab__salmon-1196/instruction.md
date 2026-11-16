# Issue

**Title:** Index format v2: sshash-rs 0.7 one-modality dictionary

## Description

Adopts piscem-rs 0.10 / sshash-lib 0.7 (COMBINE-lab/piscem-rs#6): the unified canonical minimizer scheme (C++ SSHash v6 port). `INDEX_FORMAT_VERSION` and `MIN_READABLE_INDEX_VERSION` move 1→2 — **all existing salmon indices must be rebuilt** — with actionable rejection messages in both directions (old index → 'rebuild'; future index → 'upgrade salmon'). `info.json` now records `sshash_format_version`. No salmon CLI options change.

**Validation** (rebased onto current develop, which contains the released v2.6.0): all 42 workspace suites pass; against a v2.6.0-built baseline, quant.sf and per-fragment RAD payloads are **bit-identical** on sample_data (SA + sketch), on a decoy index, and on GRCh38 × ERR188044 (193,760 transcripts, identical num_mapped). Perf: human index build −23% peak RSS / −3% wall; sketch quant −3% wall; sketch map-only −5.5% wall / −5.7% CPU. Full narrative in `docs/sshash-v6-port.md`.

**Draft until piscem-rs 0.10.0 is on crates.io** — the `[patch.crates-io]` block (piscem-rs, thread-broker, sshash-lib, tiny-dict) then comes out and CI can go green.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01NknHxdevZi243yQ5sKaffu

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1cefc2680a01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** feat(rad): libradicl 0.21 + unify noodles on 0.116 (read RAD v2 bulk)

## Description

## Summary

Moves the salmon workspace to **libradicl 0.21** and unifies the whole graph on a single, latest **noodles 0.116**. This is the salmon piece of the coordinated RAD v2 rollout and also supersedes the split dependabot noodles bumps.

## libradicl 0.18 → 0.21

- [`piscem`](https://github.com/COMBINE-lab/piscem) now emits the versioned **RAD v2** format (8-byte `RAD_FILE` magic + spec version + prelude extension block + per-tag roles) **unconditionally**. libradicl ≥ 0.20 detects and skips the prelude — the old 0.18 misreads the magic as `is_paired`/`ref_count`; 0.21 additionally reads bulk records via their declared tag **roles**. salmon-align reads bulk RAD through libradicl's `ParallelRadReader` (already role-preferring), so **no reader code change** is needed.
- Adapt salmon's own RAD **writer**/test fixtures to two libradicl API changes: non-exhaustive `TagDesc` → `TagDesc::new`, and the added `RadHeader.version` field → write `SpecVersion::Legacy` (salmon's on-disk output is byte-identical). libradicl 0.21 also dropped `from_bam_header`, but salmon never called it.

## noodles 0.115 → 0.116 (unified, single version)

- Bump the direct deps in `salmon-align` and `salmon-quant` (noodles-bam 0.95, noodles-sam 0.90, noodles-csi 0.61, gff/gtf), and **bramble-rs 0.1.8 → 0.1.9** (which moved to noodles 0.116).
- Because **libradicl 0.21 no longer depends on noodles at all** and bramble-rs 0.1.9 is on 0.116, the graph now carries **exactly one version of every noodles crate** (verified: noodles/bam/sam/csi/bgzf/core/gff/gtf each resolve to a single version; no 0.94/0.89/0.115 left).
- **Supersedes #1193 and #1194**, which each bumped only one of noodles-bam / noodles-sam and so hit a bam↔sam version skew (E0308). Please close those in favor of this PR.

## Validation

`cargo test -p salmon-align -p salmon-rad -p salmon-quant` green; `cargo fmt --check` + `cargo clippy` clean. New `piscem_bulk_v2_prelude_quantifies` test writes a bulk RAD with the v2 prelude (asserts the `RAD_FILE` magic) and confirms `quantify_rad` skips it and quantifies identically to the legacy fixture. Builds against the published libradicl 0.21.0 + bramble-rs 0.1.9.

## Note

The website build fix is a separate PR (#1218). salmon's RAD *writer* stays on the legacy (magic-less) format here — read-compat only; emitting v2 from salmon is a deliberate follow-up.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34f99a1aa6cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
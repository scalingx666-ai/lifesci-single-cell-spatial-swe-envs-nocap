# Issue

**Title:** perf(align): parallelize bias effective-length correction

## Description

## Summary

Alignment and RAD quantification apply bias-corrected effective lengths with the same per-transcript `corrected_effective_length_full` calculation as reads mode, but `salmon-align::apply_bias_correction` ran that sweep serially. On a large transcript catalog this left the abundance phase pinned to one core after the bias models had been built.

This PR:

- runs the independent per-transcript corrections through Salmon's existing Rayon pool;
- leaves the arithmetic within each transcript and the ordering of `eff_lengths` unchanged;
- preserves the dedicated GC-only `ref_seqs` regression; and
- adds a separate all-bias test requiring finite effective lengths and exact 1-thread/8-thread invariance for effective lengths, counts, TPMs, and all dumped bias models.

There is no public API, file-format, model, or default-option change.

## Scope relative to earlier bias work

The reads-mode driver already uses `into_par_iter()` for this correction sweep. This does not revisit the expected-model construction work discussed in #1020 and folded into #1017; it changes only the separate serial sweep in the later alignment/RAD `apply_bias_correction` path.

## Why the parallelism is output-preserving

Each iteration reads shared immutable bias models and reference sequence, performs the existing calculation for one transcript, and writes one disjoint `eff_lengths[tid]` slot. There is no cross-transcript reduction, so thread scheduling cannot change floating-point evaluation order within a transcript.

## Performance

Measured with a release build on a deterministic real-data RAD subset containing 471,017 records while retaining the full 655,022-reference catalog and reference/bias workload:

| threads | correction sweep |
| ---: | ---: |
| 1 | 42.306 s |
| 2 | 22.638 s |
| 4 | 13.438 s |
| 8 | 8.508 s |
| 16 | 6.381 s |

That is 6.6x scaling for the corrected-effective-length sweep at 16 threads.

In an interleaved A-B-B-A comparison at 16 threads:

| measurement | serial baseline | parallel candidate | change |
| --- | ---: | ---: | ---: |
| bias/abundance phase mean | 86.98 s | 51.35 s | -41.0% |
| end-to-end wall mean | 124.95 s | 92.35 s | -26.1% |

Peak RSS was effectively unchanged (approximately 10.46 million KiB in both cases). `quant.sf` and `quant.genes.sf` were byte-identical; the 1/2/4/8/16-thread candidate runs also produced the same quantification SHA-256.

As a larger supporting check, one 17.4M-fragment run decreased from 7:31.6 to 5:10.0 and produced identical quantification and bias-model artifacts. I treat that timing only as supporting evidence because unrelated background services made the host load less controlled than the A-B-B-A run above.

## Verification

- `cargo fmt --all -- --check`
- `cargo clippy --workspace --all-targets -- -D warnings`
- `cargo test --workspace --release` (all tests pass; one profiling benchmark remains ignored as intended)
- `git diff --check origin/master...HEAD`
- the all-bias regression requires finite effective lengths and exact 1-thread/8-thread equality
- exact real-data output parity across thread counts and against the serial baseline

AI-assisted implementation disclosure: OpenAI Codex assisted with implementation, review, testing, and benchmarking; the reported commands and artifacts were executed and checked locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca16791e58b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
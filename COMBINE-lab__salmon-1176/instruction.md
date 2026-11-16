# Issue

**Title:** perf(infer): reuse a persistent high-thread EM phase queue

## Description

Depends on #1172.

## Summary

Replace repeated high-thread fork-join task construction in long unaccelerated EM/VBEM loops with one persistent Rayon broadcast and a completion-counted phase queue. The queue is selected only at 32+ Rayon workers and 32+ allowed iterations; smaller pools, short loops, bootstrap replicates, SQUAREM, and DAAREM keep the existing path.

Logical shards and fixed 2,048-transcript chunks do not depend on the pool. Workers dynamically claim complete jobs, and the last completed job publishes the next phase. There is no all-worker barrier and no atomic floating-point addition, so the existing deterministic arithmetic grouping is unchanged.

## Five-run RAD A/B

Baseline is #1172 production commit 04c0a93b; candidate production commit is 2be15176. Both hosts used the documented 26.1M-fragment/Gencode v49 RAD, alternating arms, and physical-core-first affinity. Values are median EM phase time.

| host | threads | baseline | candidate | change |
|---|---:|---:|---:|---:|
| 2x EPYC 9575F | 16 | 5.504 s | 5.613 s | +2.0% (fallback) |
| 2x EPYC 9575F | 32 | 5.127 s | 3.903 s | -23.9% |
| 2x EPYC 9575F | 64 | 6.298 s | 2.836 s | -55.0% |
| 2x Xeon E5-2699 v4 | 16 | 12.362 s | 12.395 s | +0.3% (fallback) |
| 2x Xeon E5-2699 v4 | 32 | 9.976 s | 8.151 s | -18.3% |
| 2x Xeon E5-2699 v4 | 64 | 11.362 s | 8.043 s | -29.2% |

The 16/32/64 geometric mean improves 29.6% locally and 16.6% on newton. Local 16-to-64 scaling changes from 0.874x to 1.980x; newton changes from 1.088x to 1.541x. Newton remains nearly flat from 32 to 64 because the 64-thread affinity includes 20 SMT siblings after its 44 physical cores; the release-note wording calls this out rather than claiming linear scaling.

Generic perf counters show aggregate cycles falling 31%/66% locally and 14%/30% on newton at 32/64 threads. Median RSS is essentially unchanged. Raw runs, counters, commands, rejected barrier variants, and a scaling curve are committed under docs/benchmarks/em-thread-scaling/ and summarized in docs/em-architecture-and-optimization.md.

## Determinism and validation

- Every baseline and candidate run on each host has the same quant.sf SHA-256 across all measured thread counts.
- All runs converge in 2,811 iterations; equality to the already-validated #1172 output preserves finite/nonnegative counts and conserved mass.
- A direct 50-step test requires bit-identical persistent vs repeated fork-join results for both EM and VBEM.
- Complete EmResult determinism now includes a 32-thread pool, in addition to 1/2/3/8/16 and the existing EM/VBEM, per-nucleotide, SQUAREM, and DAAREM configurations.
- Empty equivalence classes and zero-job phases are covered.
- cargo fmt / diff check pass.
- cargo clippy --workspace --all-targets -- -D warnings passes.
- cargo test --workspace --release -- --test-threads=1 passes, including doctests.

## Rejected prototypes

Fixed shard ownership with a blocking barrier regressed 16 threads by roughly 40%; dynamic shards with a blocking barrier still regressed by about 14%; spin and hybrid barriers were unstable under worker preemption and competed with the 64-thread memory-bound phase. The selected completion-counted queue removes the requirement that every worker rendezvous between phases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e2e675877a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
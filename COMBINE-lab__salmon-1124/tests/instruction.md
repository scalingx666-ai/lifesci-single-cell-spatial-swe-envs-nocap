# Issue

**Title:** perf(infer): parallelize the serial exp_theta fill in the VBEM step

## Description

I profiled the Salmon code and found that `fill_exp_theta` function is the best target for optimization. It was the only remaining serial loop in the VBEM M-step.


* I ran multiple tests on m8a.4xlarge AWS VM in docker on different samples (see table below) in order to test performance improvement and validate that change does not affect output of Salmon. For that I also used the `--deterministic` flag. Usually run with `-p 14` and for validation also with `-p 1`.
* Under `--deterministic` the output is byte-identical to the unmodified build on every library I tested — `quant.sf`, `aux_info/`, `libParams/` and `lib_format_counts.json` — at `-p 14` and at `-p 1`. The `-p 1` output also matches the `-p 14` output, so thread-count invariance is preserved.
* Salmon's test suite passes: 30 test binaries, 277 tests, 0 failures.
* Peak RSS is unchanged, within measurement error.
* I used salmon 2.5.0, but `packed.rs` is byte-identical in v2.5.1.
* Without `--deterministic` the same library (DRR122028) runs 1.18× faster end to end, inference phase 2.62×. Byte-identity is not testable in that mode

Two unpatched reference runs and three patched runs per library, medians. 
| library | pairs | mapped | inference share | total time | end to end | saved |
|---|---|---|---|---|---|---|
| DRR306484 | 5.9 M | 90.6% | 52.3% | 22.4 s → 14.9 s | **1.499×** | 7.4 s |
| SRR1039508 | 22.9 M | 94.9% | 47.2% | 56.9 s → 43.4 s | **1.311×** | 13.5 s |
| DRR122028 | 27.1 M | 93.0% | 20.2% | 66.3 s → 57.9 s | **1.146×** | 8.5 s |
| DRR182998 | 32.8 M | 76.5% | 11.3% | 179.6 s → 167.8 s | **1.070×** | 11.8 s |
| DRR015468 | 17.6 M | 75.4% | 6.9% | 169.4 s → 162.4 s | **1.044×** | 7.1 s |
| DRR024811 | 12.2 M | 63.1% | 4.8% | 226.7 s → 220.1 s | **1.030×** | 6.6 s |
| ERR10823160 | 12.2 M | 21.0% | 2.6% | 118.3 s → 116.4 s | **1.017×** | 1.9 s |
| DRR228539 | 69.6 M | 64.5% | 1.2% | 832.8 s → 826.8 s | **1.007×** | 6.0 s |

Aggregate: 1672 s → 1610 s, 62.8 s saved.

* This was done as part of my experimenting with OpenEvolve (https://github.com/algorithmicsuperintelligence/openevolve/tree/main) and automated the evaluation with Claude. I think this is descriptive enough to be considered and hopefully merged but I can provide more details if necessary.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c360459bbf16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
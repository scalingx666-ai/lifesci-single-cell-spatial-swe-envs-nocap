# Issue

**Title:** perf(infer): faster EM/VBEM component step (bit-identical)

## Description

## Faster EM/VBEM component step, bit-identical

Two small changes to the component engine's single-threaded push step in `salmon-infer`. Both leave every result bit-for-bit unchanged.

1. **Plain EM:** drop the per-incidence bounds checks and the per-product NaN test.
   - Every class label is a component-local transcript id. This is now asserted once, when the plan is built, so the step can index unchecked.
   - The checked step skips a NaN product, but a NaN product always leaves a NaN in `next`. The fast step's output is scanned once per step; if it contains a NaN, the step is recomputed with the checked kernel from the same input. Otherwise both kernels add the same terms in the same order.
2. **VBEM:** with a prior of at least 0.002 (the default is 0.01), the zero-expectation guard is off and the step adds every product. That is the same computation over the expectations, so it uses the same unchecked step.

Measured on the GENCODE v50 muscle RAD (SRR13638690), EM time only:

| | before | after |
|---|---|---|
| plain EM, 1 thread (1420 iterations) | 6.62 s | 6.18 s |
| plain EM, 8 threads | 0.98 s | 0.93 s |
| VBEM, 1 thread | 1.013 s | 0.968 s |

The main motivation is piscem-infer, which uses plain EM by default and will build on this release. In salmon the EM is a small share of a run.

### Checked
- `quant.sf` is byte-identical to the 2.9.0 release on muscle `--sketch -p 8`, both default VBEM and `--useEM`.
- piscem-infer output is identical at `--num-threads 1` and `8`.
- `cargo test --release --workspace --locked`: 383 passed. Clippy (`-D warnings`) and fmt are clean.

### Tried and dropped (for the record)
- Skipping components at an exact fixed point: under 0.4% of the work, no gain.
- Summing four classes' denominators side by side: exact, but 6% slower. The add latency isn't the bottleneck.

Intended for a 2.9.1 patch release, so piscem-infer 0.8.0 can depend on it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `506305baae6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
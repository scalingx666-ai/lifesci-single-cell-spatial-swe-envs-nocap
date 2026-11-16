# Issue

**Title:** refactor(model,infer): delete unused bias and EM code and test the production path

## Description

## Problem

Production computes bias-corrected effective lengths only through `corrected_effective_length_full`, but no unit test called it. The tests covered two older copies, `corrected_effective_length` and `corrected_effective_length_fft`, so a bug in the real function could pass. That is how the floor mismatch in #1289 survived.

The EM crate carried similar leftovers:

- `optimize_with_init` had no callers.
- The plain M-step loop for `EmAccel::None` could only run with no classes, because `run_em_counts` sends every other unaccelerated run to the component engine first. With `max_iter = 0` its body never ran.
- That loop was the only user of the convergence check threaded through the parallel kernels (`RelDiffCheck`, `max_of`, and the second return value), so a hot path carried a parameter that nothing needed.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit traced the callers by grep and read the dispatch in `run_em_counts`. I re-checked each item on `develop` before deleting it. `RelDiffCheck` was still in use, but only by the loop being removed, so it goes with it. Tracked in #1283 (finding 20).

## Change

About 200 net lines removed.

- **Deleted:** `corrected_effective_length`, `corrected_effective_length_fft`, `optimize_with_init`, the plain loop, `RelDiffCheck` and the kernels' check parameter.
- **Tests repointed at `corrected_effective_length_full`:** `unbiased_correction_reduces_to_standard_eff_len` and `fft_matches_exact_scalar_corrected_eff_len`. The second now compares the two production paths: sequence bias alone takes the cross-correlation, and adding a GC model whose every ratio is 1 selects the scalar loop without changing the answer.
- **`EmAccel::None` arm:** it now answers the two remaining cases directly. With no classes, abundances are zero and the run counts as converged. With `max_iter = 0`, the start is returned unchanged.

`corrected_effective_length` was publicly re-exported from `salmon_model`, and `corrected_effective_length_fft` and `optimize_with_init` were public too. They had no callers in this workspace, but an outside user of these crates would need to move to `corrected_effective_length_full` or `optimize_packed_with_init`.

## Behaviour change

One reported value: an empty input now reports 0 EM iterations rather than 50. Abundances and the converged flag are unchanged.

## Verification

- I compared `quant.sf` from a binary built before and after this change on a synthetic 40-transcript, 20000-pair dataset. The output was byte-identical for: default, `--useEM`, `--emAccel squarem`, `--useEM --emAccel daarem`, `--seqBias`, `--gcBias`, and `--seqBias --gcBias --posBias`.
- New test `empty_input_and_zero_iterations_need_no_m_step` in `crates/salmon-infer/src/lib.rs`. It passed on the old code before the deletion, so it pins the behaviour rather than a bug.
- `cargo test --workspace` passes on this branch, and workspace clippy is clean with `-D warnings`, including the benches.
- I did not measure speed. Removing a branch from the kernels should not slow them, but `benches/em_step.rs` was only compiled, not run.
- This overlaps #1289 in `seqbias.rs`, so whichever merges second needs a small rebase.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
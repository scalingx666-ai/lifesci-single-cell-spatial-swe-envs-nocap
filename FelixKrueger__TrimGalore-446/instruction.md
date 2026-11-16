# Issue

**Title:** perf(clump): refit the --clumpify memory model against measured peak RSS

## Description

Phase 2 of #439, on top of #442. Phase 1 cut actual memory; this refits the *sizing model* against measured peak RSS, so the printed prediction now bounds reality instead of under-charging. σ = 23/16 and k = 4 per worker come from a 10 M-pair paired matrix over `--cores 2–4` with `n_bins` pinned, worst of two reps per cell, with `--cores 8` and `16` held out and predicted within 5%; the flat 512 MiB reservation becomes 224 MiB plus 24 MiB per FastQC thread, capped at 16. Full matrix and raw data in `plans/08162026_clumpify-memory-accounting/phase2/CALIBRATION.md`.

Peak RSS as a fraction of the printed budget, worst of two reps, 10 M distinct-read pairs:

| cell | macOS | Linux | was (Phase 1) |
|---|---|---|---|
| `--memory 1G --cores 4` | 0.862 | 0.747 | 1.008 |
| `--memory 2G --cores 4` | 0.887 | 0.797 | **1.014** |
| `--memory 1G --cores 8` | 0.828 | 0.766 | 0.959 |
| `--memory 1G --cores 4 --fastqc` | 0.739 | 0.682 | — |
| `--memory 2G --cores 16 --fastqc` | 0.682 | — | — |

`cores` also stops doing three jobs at once — it now splits into the count that drives `n_bins` (pinned, so bin grouping doesn't shift), the workers that can hold batches, and FastQC's real thread count. That fixes two live holes: `--fastqc_args "-t 16"` reserved for `--cores` while FastQC ran 16 threads, and `--clump_only` (synchronous) was charged for workers it never starts, squeezing bins to 2.07 MiB at `--cores 16 --fastqc`.

**Behaviour change worth knowing:** `--clumpify` output is no longer byte-identical to the previous release. Bins at the default cell move 18.96 → 18.13 MiB, which shifts gzip member boundaries and grows output 0.27% / 0.24% on a 10 M-pair run. The record multiset is unchanged — same data, different framing.

<details>
<summary>Review findings applied, and what is still outstanding (AI-assisted work — bin freely)</summary>

Dual code review plus a coverage audit ran against this change; reports are in the plan directory. Both reviewers independently brute-forced the two load-bearing properties and confirmed them: the predicted peak never exceeds the budget (swept to `u64::MAX` × cores 1…2²⁰ × fastqc, zero violations), and the advertised floor is the *least* resolvable budget.

Applied from review: the below-floor warning was advertising a `--memory` that fails on retry (it truncated to MiB where the sibling bail message rounds up — 124 of 126 sampled cells), and the floor test now asserts the advised MiB figure resolves, not just the byte-exact floor. Two bail tests were inert — they passed under all 17 perturbations of the constants, including reverting the static to 512 MiB — and now sit one byte under the floor. Two tests were added for the per-thread scaling and the worker split, which previously had nothing that could see them.

One recorded deviation: `CALIBRATION.md` recommended treating FastQC as a `max` rather than an addend. This ships an addend, because the pool's pages stay resident across the trim→FastQC boundary under mimalloc — at `--cores 16` with only 64 MiB of pool the process peaked at 438.8 MiB, i.e. the trim reservation plus ~215 MiB. The spec is the document that needs amending, and the plan now says so.

Still outstanding, both deliberately: `--clump_only` propagates a layout error rather than warning and falling back, so a below-floor budget aborts there instead of degrading — a behaviour decision, and the floor it would abort on is *lower* than before for every non-FastQC configuration. And Phase 3 remains: a CI guard that would defend this promise mechanically, plus the arithmetic in `docs/performance/clumpy.md`, which is wrong in nine places (formula, both worked values, the floor range, the sample warning, and MB/MiB units).

Unverified axes: single-end, multi-pair, and short-read length (σ rises to ~1.55 on 25 bp records against a coefficient of 1.4375, which the 9% margin covers but with less room than elsewhere).
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d075f9bade4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
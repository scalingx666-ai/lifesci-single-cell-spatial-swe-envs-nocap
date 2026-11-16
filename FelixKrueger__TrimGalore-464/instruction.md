# Issue

**Title:** feat(clump): print --clump_only's predicted peak, like --clumpify

## Description

.

`--clumpify` names its predicted peak and the budget it came from; `--clump_only` printed only its bin layout. That left the memory visibility added under #439 missing from the mode where it matters more — `--clump_only` fails below the memory floor rather than falling back to plain mode, so a user had no way to see how close they were before it did.

```
before: clump-only: reordering 'in.fq.gz' -> 'in_clumped.fq.gz' (16 bins × 26 MiB each, gzip level 1)
after:  clump-only: reordering 'in.fq.gz' -> 'in_clumped.fq.gz' (16 bins × 26 MiB each; predicted peak ≈ 930 of 1024 MiB budget, gzip level 1)
```

<details>
<summary>Detail (AI-assisted)</summary>

`ClumpLayout::predicted_peak_bytes()` and `memory_budget_bytes` were both already in scope at all four sites, so this is a format argument and no model work — as the issue predicted.

**All four banners are pinned separately.** Removing the figure from any one of them turns exactly one test red, verified by mutating each in turn:

| banner | test that goes red |
|---|---|
| `clump-only: reordering` | `banner_reports_the_predicted_peak` |
| `clump-only (paired)` | `banner_reports_the_predicted_peak` |
| `clump-only (uBAM out): reordering` | `ubam_out_banners_report_the_predicted_peak` |
| `clump-only (uBAM out, paired)` | `ubam_out_banners_report_the_predicted_peak` |

The two uBAM shapes are covered in `integration_clump_only_ubam.rs` rather than folded into one test, because a single test over one shape would let the other three regress green.

Both figures are asserted **by value** (`930 of 1024`), matching how the existing `--clumpify` assertion in `integration_preflight_tripwire.rs` pins the same arithmetic — at the default `--memory 1G`, 1024 × 10/11 truncates to 930, so a divisor change is caught where a unit label alone would not be.

`--clumpify`'s own banner is byte-unchanged. 798 tests (2 new), `fmt` and `clippy --all-targets --release -D warnings` clean.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45876c59df8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
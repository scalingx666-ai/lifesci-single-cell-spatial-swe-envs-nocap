# Issue

**Title:** perf(clump): cut --clumpify peak RSS 13-17% and label the banner MiB

## Description

Phase 1 of #439. `--clumpify` printed a predicted peak and sized its bin pool to stay inside `--memory`, but didn't: at `--memory 1G --cores 4` on macOS/arm64 it peaked above the 1024 MiB it promised, and the overshoot grew with the budget. Two structural changes cut peak RSS 13–17% without touching output bytes — the clumpy work channel drops to depth 1 (plain round-robin keeps depth 2), and each per-batch output buffer is reserved from its own mate's record bytes rather than a flat 300 B/record.

Measured on 6.81M read pairs, macOS/arm64, paired, `--compression 6`, worst of 2 runs, against `2ab0918`:

| cell | peak RSS | ratio to the printed budget |
|---|---|---|
| `--memory 1G --cores 4` | 1034 → 884 MiB | 1.008 → **0.863** |
| `--memory 2G --cores 4` | 2403 → 2077 MiB | 1.173 → **1.014** |
| `--memory 1G --cores 8` | 983 → 818 MiB | 0.959 → **0.798** |
| plain, `--cores 4` | 97 → 91 MiB | (no budget printed) |

Output is byte-identical to `2ab0918` on both the clumpy and plain paths; CPU time moves +0.5% in plain mode, and wall-clock variance on the test host is an order of magnitude larger than any effect here.

**This does not close #439.** `2G/c4` lands at 1.014, and `predicted_peak_bytes` still charges one in-flight batch per worker where two can now be resident. The model docstring states that under-estimate explicitly; the calibration is Phase 2.

Also in here: five banner figures divided by 1024² while printing `MB` and now print `MiB` (guarded by an assertion that pins both labels), `ClumpLayout` carries the core count it was sized for so the prediction can't be evaluated against a different one, and a new test pins the resolved bin budget at `1G/--cores 4` so no future coefficient edit moves that cell silently.

<details>
<summary>Notes from review (AI-assisted work — bin freely)</summary>

The buffer-reserve change is **tidiness, not a memory lever**, which is a correction to how I first described it. Mean record bytes are 338 on 150 bp reads against the flat 300 it replaces, so above ~125 bp the reserve grows rather than shrinks. It is an exact bound in the plain branch and removes the doubling cascade long reads used to trigger; in clumpy mode it is near-neutral, because every clumpy run is a gzip run and large over-reserves get mmapped without being faulted in. That last point also explains why it saved 47 MiB at 1G but only 4 MiB at 2G.

`--clump_only` bypasses the warn-and-fall-back path and propagates a layout error directly, so a future floor change would abort it rather than degrade it — ~23 integration invocations run at the default budget. Nothing here moves the floor, so that decision is deferred rather than guessed.

Logged for later, all pre-existing or out of scope: `docs/performance/clumpy.md` quotes the banner as "32 bins × 12 MB", which was already wrong against the shipped formula before the unit change; and `docs/performance/threading.md` claims memory "never exceeds ~100 MB" against 802 MiB measured in plain mode at `--cores 4` on 10 kb reads, because `BATCH_SIZE` is 4096 *records* regardless of read length. The second looks worth its own issue — it is unbounded in read length and sharper for ONT/PacBio users than #439.

Plan, dual plan reviews (two rounds), the spike report, dual code reviews and the coverage audit are in `plans/08162026_clumpify-memory-accounting/`, uncommitted as usual for plan artifacts.
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ab0918644aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** perf(rad): tally RAD records per worker, merge once per thread

## Description

.

#1099 handled the read-based path: five of the seven per-fragment counters became per-worker `u64`s merged once per thread. Two remain shared there and are structurally required — `num_mapped` and `num_processed` are *read* while the run is in flight (the `use_aux` gate and the CLI progress bar), so a thread-local tally merged at thread end would read zero all run. That is documented on the issue.

This PR does the one acceptance criterion that was never addressed: **the RAD worker loops**.

### What changed

`RadTallies::tally` performed up to three shared-atomic RMWs per record — `records`, `mapped`, `orphans` — in both `run_rad_pass` and the fused `run_rad_eq_and_bias_pass`. `LocalTallies` accumulates the same three counts in plain `u64`s and folds them into the shared atomics once per worker, guarded by `if v != 0`. That is the pattern `BiasLocal` already uses in the fused pass.

These are safe to localise in a way the quant-side pair is not: **nothing reads them while the run is in flight**. They are consumed once, after every worker has joined, through `into_inner()`.

### Correctness

10M human fragments from a salmon RAD, at `-p 1`, `-p 8` and `-p 16`, against develop:

- every `meta_info.json` counter identical in all six runs — `num_processed` 9,221,625 · `num_mapped` 9,221,625 · `num_orphan` 623,154 · `percent_mapped` 100.0
- `quant.sf` identical at every thread count

So the merge is thread-count independent as well as correct.

### Performance

Interleaved A/B against develop, 10M-fragment RAD, warm-up round discarded, at the thread counts the issue asks for:

| threads | develop | this PR | delta | t | 95% CI | faster |
| ---: | ---: | ---: | ---: | ---: | :---: | :---: |
| 1 | 23.994s | 24.295s | **+1.25%** | +3.70 | [+0.138, +0.463]s | 5/18 |
| 8 | 13.460s | 13.035s | **−3.16%** | −4.76 | [−0.604, −0.247]s | 15/18 |
| 32 | 12.124s | 11.947s | **−1.46%** | −2.06 | [−0.349, −0.005]s | 9/14 |

At 8 and 32 threads this is a real win, and the direction matches the issue's contention argument — which is notable, because almost every other structural item in #1092 measured null.

**The `-p 1` row is a genuine anomaly and I am not going to explain it away.** With a single worker there is no contention to remove, so the honest expectation is "neutral", not "1.25% slower" at t=3.70. I do not have a mechanism for it beyond code layout — adding a struct and a merge call perturbs inlining and alignment, which routinely moves timings a percent or so with no logical cause. An order-swap control is running (the main run always executed develop first) and I will post the result here. If it is a real regression at `-p 1` it is worth weighing against the gains at 8 and 32, since `--rad -p 1` is not a common configuration but is not absurd either.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6243fcfc7451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
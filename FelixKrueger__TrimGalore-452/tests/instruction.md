# Issue

**Title:** ci(clump): measure --clumpify peak RSS on every PR

## Description

Nothing in CI measured resident memory, so a refactor could restore the under-charging the earlier #439 phases removed and leave all nine checks green. This adds a job that measures peak RSS on a generated 10M-pair gzipped fixture and gates on two things: the *promise* (measured peak ≤ the peak the binary printed, absolute and platform-independent) and *drift* (peak/prediction within a recorded band, because the promise alone cannot catch a channel-depth revert on Linux). It also retires `resolve_layout_predicted_peak_fits_budget`, which the parent plan assigned to this phase on condition the replacement existed first — so it goes in the PR that adds it.

Stacked on #451; review that one first.

<details>
<summary>Detail (AI-assisted)</summary>

**Why a band and not just the promise.** At the expected ~0.85 Linux ratio, restoring the clumpy work-channel depth adds 72–104 MiB and still lands under the 930 MiB printed prediction — green forever. The band fails above `baseline + 0.05` (a depth revert is a 0.08–0.11 move, so it breaches on any platform) and below `baseline − 0.10` (a silent fallback to plain mode, or a fixture that stopped filling the bin pool). Baselines live in `.github/clumpify-memory-baseline.tsv`, currently in a `BOOTSTRAP` mode that records and warns; the marker prints on every run so it cannot sit there unnoticed.

**Fixture size is the design, not a cost dial.** Measured ratios climb monotonically with pair count — 0.38 at 500K, 0.75 at 1.5M, 0.80 at 3M, 0.88 at 6M, ~0.95 at 10M — so anything smaller yields a job that cannot fail. Gzipped because output encoding follows the input's and the plain-output branch is not what users run; it is also the more sensitive arm and a sixth of the disk.

**Disk is not independent of memory.** A stalled writer backs up the result channel and the `pending` map, both of which hold written-but-unflushed buffers, so an out-of-space run reports inflated peak RSS and presents as a model breach — the most expensive false positive available here, since the obvious response is to loosen the gate. The job asserts ≥8 GiB free up front, truncates each cell's output before the next, and checks every exit status. `/usr/bin/time -v` exits with the child's status, but piping into a filter replaces it, and a filter succeeding on a failed run's parseable banner is exactly the trap — so the job captures to a file, checks status, then parses.

**Cells.** `1G/c4` and `1G/c4 --fastqc` gate on the promise. `25bp/1G/c4` is recorded only: it exceeds the prediction today because the per-bin coefficient is fitted per byte rather than per record, so short reads pack more records into the same bin bytes. `multipair_c4` needs distinct paths to the same bytes (one pair twice is refused as a duplicate) and prints one banner per pair, so the parse takes the first — the promise is per-process.

**The retired test.** It asserted `predicted ≤ budget` over five cells, which reduces to `MARGIN_NUM ≤ MARGIN_DEN` and passes for any coefficients; #446 made it more vacuous still, the chain now being `predicted ≤ budget × 10/11 ≤ budget`. Its replacement is this job plus #451's pinned-cell table.

Verified: 789 tests pass, fmt and clippy clean (`--all-targets` covers the new example). Workflow YAML parsed. `sed` patterns are POSIX rather than GNU-only so they could be tested locally: verified they parse a real banner, take the first of two banners on the multi-pair log, and that the empty-field guard fires on a truncated log.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `242546ad248f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
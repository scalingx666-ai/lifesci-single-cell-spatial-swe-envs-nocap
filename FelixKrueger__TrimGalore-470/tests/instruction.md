# Issue

**Title:** ci(clump): measure `--memory 2G`/`--cores 4` instead of recording it as a blind spot

## Description

Closes the blind spot #458 exists to record, rather than leaving it recorded.

`2G/c4` carried #439's original breach — 1.173 → 1.014 → 0.887 of budget across the two fix phases — and came out of that work with **neither a CI cell nor any continuing measurement**. #458 was filed so it would be rediscovered as a known item rather than as novel, and concluded "no action required".

**The reason it was dropped was a gating argument.** Its 672 MiB pool (16 × 42 MiB) needs ~2.3× the job's fixture to reach steady state, making it the least informative candidate per byte for a cell that must be able to fail the absolute promise. That reasoning is sound, and it does not transfer to a **recorded** cell: those only need to be reproducible, and this one reuses the existing `f51` fixture at no generation cost.

One correction to a guess I made before checking: `2G/c4` is not a weak drift detector. `B` = 16 × (2048 × 10/11 − 224) / 624 = **42.0 MiB**, against 18.1 MiB at `1G/c4`, so lever A moves its ratio **+0.090 to +0.130** — essentially the same proportional sensitivity as the cell the band is centred on.

**Non-gating and unbanded on first appearance**, as with every cell added since the band went live: its dispersion is unknown, and the two-sided rule needs a double-digit sample before a width can be chosen. The expected *low* ratio is documented in the baseline file so a future reader does not mistake the depression for headroom.

Cost: one more measured cell on an existing fixture, no new generation, no new dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d773131a285d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
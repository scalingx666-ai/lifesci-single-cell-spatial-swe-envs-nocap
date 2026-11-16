# Issue

**Title:** ci(clump): re-tune the clumpify drift band on 27 observations per cell

## Description

The drift band added in #462 was calibrated from **four reps per cell**, and four draws estimate dispersion low by construction — they cannot land far apart as often as they can land close. The resulting `+0.05` width was narrower than the runner's real spread, and it false-fired on an unrelated PR: `multipair_c4` at 0.852 against a 0.840 trigger, moving alone while `1G_c4` went +0.012 and `25bp_1G_c4` −0.019. The re-run passed with no code change.

Recomputed from **27 observations per cell** (31 job logs, excluding Validation 8's two deliberately-regressed runs):

| cell | n | mean | min | max | range | width for 3× half-range | banded |
|---|---:|---:|---:|---:|---:|---:|---|
| `1G_c4` | 27 | 0.7883 | 0.770 | 0.825 | 0.055 | 0.083 | **yes, 0.788** |
| `25bp_1G_c4` | 27 | 0.9138 | 0.898 | 0.941 | 0.043 | 0.065 | **yes, 0.914** |
| `multipair_c4` | 27 | 0.7987 | 0.771 | 0.852 | 0.081 | 0.121 | no |
| `1G_c4_fastqc` | 27 | 0.7069 | 0.688 | 0.768 | 0.080 | 0.120 | no |
| `1G_c2` | 25 | 0.8789 | 0.860 | 0.894 | 0.034 | 0.051 | no |
| `25bp_1G_c2` | 25 | 1.0301 | 1.007 | 1.050 | 0.043 | 0.065 | no |

**No cell cleared the 3× bar at `+0.05`** — including all three that were banded on it — and `1G_c4` had already come within 0.002 of firing at 0.825.

**Widening is affordable because the regression was measured rather than predicted.** Validation 8 put a work-channel-depth revert at **+0.126 to +0.151** of prediction, where the original sizing assumed the predicted +0.078. At `+0.09` both remaining banded cells clear 3× (3.3× and 4.2×) and still red on that regression by 0.036 and 0.038.

`multipair_c4` is **unbanded**: covering its 0.081 range at 3× would need a width close to the regression the band exists to catch. It stays measured, and since a depth revert moves every cell together, either banded cell catches it — the same argument that already excluded `1G_c4_fastqc`.

**The rule is now two-sided**, which is the actual defect being fixed:

```
width >= 3x the observed half-range      (so noise cannot fire it), and
width <= the measured regression delta   (so the regression still fires it),
         minus a working margin
```

…with the half-range required to come from a double-digit sample. As originally written it constrained only the noise side, and was evaluated with the very estimate it was meant to guard against.

**Verified against the committed clauses, not a paraphrase:** all 54 observations of the two banded cells pass; both red at the measured lever-A deltas; the strict-`>` boundary holds (`+0.090` passes, `+0.091` fires); the lower bound is still live; unbanded cells are not checked; and the armed-check still catches a deleted row while correctly accepting a deliberately-unbanded cell that happens to have a row.

No CHANGELOG entry — CI-only, matching #452 and #462.

Part of #439 (closed; this corrects the guard it shipped).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e86e2afbe5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
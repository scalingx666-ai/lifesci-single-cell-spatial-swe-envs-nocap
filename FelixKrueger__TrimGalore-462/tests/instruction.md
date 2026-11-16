# Issue

**Title:** ci(clump): enforce the clumpify drift band, and assert it stays armed

## Description

The `clumpify-memory` baseline file leaves BOOTSTRAP mode, so `peak/prediction` is now gated against a recorded band as well as against the prediction the binary prints. Gating on the printed prediction alone cannot see a work-channel-depth revert on Linux — it adds 72–104 MiB and still lands well under the prediction at the measured 0.78 ratio, which is why #439 accepted a committed baseline file in the first place.

Three cells are banded rather than all six, by a stated rule: **≥ 3 reps that predate this PR, and a false-red multiple ≥ 3×** — a spurious red must need an excursion at least three times the largest yet observed for that cell. Reps from the adding PR do not count toward the bar, or a cell would certify itself.

| cell | baseline | reps | range | false red needs | banded |
|---|---:|---:|---:|---:|---|
| `1G_c4` | 0.777 | 5 | 0.015 | 6.7× | yes |
| `25bp_1G_c4` | 0.923 | 5 | 0.029 | 3.4× | yes |
| `multipair_c4` | 0.790 | 5 | 0.021 | 4.8× | yes |
| `1G_c4_fastqc` | — | 5 | 0.048 | 2.1× | no — spread |
| `1G_c2` | — | 3 | 0.027 | 3.7× | not yet — see below |
| `25bp_1G_c2` | — | 3 | 0.017 | 5.9× | not yet — see below |

`1G_c4_fastqc` read 0.697 / 0.701 / 0.707 / 0.745 / 0.701 — the widest range of the six, having looked like the tightest on two reps. A ±0.05 band would trigger at 0.7625 against an observed max of 0.745, so banding it would go red on correct code. It stays gated on the printed prediction (0.745 of 1.000). Because a depth revert moves every cell at once, a miss needs every banded cell to miss, and `1G_c4` carries that direction at 3.7×.

The two `--cores 2` cells now clear the multiple, but only on a rep produced by this PR, and `25bp_1G_c2` tripled its range on that draw (0.005 → 0.017). Both wait for an independent confirmation — which is the rep-count bar doing its job rather than an oversight, and the file says so.

Deleting the `BOOTSTRAP` line also removes the warning that the band is off, so three silent routes to an inert band open at the same moment: a missing baseline file (the `grep` sits inside an `if`, so `set -e` does not catch it), a label typo, and a cell renamed in `ci.yml` but not in the TSV. An explicit `BANDED` list, a file-exists guard and an exactly-one-row assertion close all three, plus the duplicate-row case where `awk` would quietly coerce the first of two.

Verified against the committed clauses rather than a paraphrase of them: the band fires above **and** below with distinguishable messages (`+0.050` passes and `+0.051` fires, since the comparison is strict `>`), lever A's weakest form goes red on all three banded cells, and all five armed-check failure modes are caught — deleted row, typo'd label, renamed file, duplicate row, and a cell renamed in `ci.yml` only.

This PR's own run is the first time the band has ever been enforced; all three banded cells landed inside with 3.2–4.4 points of margin.

**Note for anyone touching `src/clump.rs`, `src/parallel.rs`'s channel depths or `src/fastqc.rs`'s thread resolution:** from this PR onward a clumpify memory regression fails CI. If a change legitimately moves peak RSS, move the baseline in the same PR and say why in the commit message.

Follows #452. Part of #439.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51fa55e6a6af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
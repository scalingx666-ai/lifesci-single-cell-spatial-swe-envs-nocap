# Issue

**Title:** feat(fld): estimate the fragment-length distribution from every concordant pair

## Description

## Fragment-length distribution from every concordant pair, not just unique ones

The deterministic fragment-length distribution (FLD) was estimated from uniquely-mapped proper pairs only. That sample is biased long: short fragments fall more often in exons shared by several isoforms, so they map ambiguously and were left out.

Now each concordant fragment adds one length:
- a uniquely-mapped fragment adds its only length, as before;
- a multi-mapping fragment adds the **shortest** length any of its placements implies. Ties go to the lowest transcript id, so the mapping pass and the RAD reader pick the same placement.

The longer alternatives usually come from isoforms that retain an intron or extend an exon between the mates, so the shortest is usually the true length.

Library-type detection (`-l A`) still counts unique fragments only, because an ambiguous fragment's placements can disagree on orientation.

The same rule applies in every path that builds the deterministic FLD:
- the mapping pass;
- the `!use_online` branch of `record`;
- RAD re-derivation (`--fldPolicy derive`, piscem RADs);
- BAM input;
- genome projection.

A FLD baked into a RAD file therefore still matches one re-derived from it. The `--online` acceptance-sampling FLD is unchanged.

### Accuracy of the distribution
On a 4M-pair Ensembl simulation (`-l ISR`), where every fragment's true length is known:

| estimator | fragments used | mean | sd | histogram L1 error vs truth |
|---|---|---|---|---|
| truth (all concordant fragments) | | 180.52 | | 0 |
| unique only (before) | 29% | 182.95 | 39.24 | 0.048 |
| **shortest implied length (this PR)** | all concordant | **180.34** | 39.26 | **0.0056** |

On the three GENCODE v50 simulations, the estimated means drop by 4–6 bp. There's no per-fragment truth for those, but the drop is in the expected direction.

On real data the bias can run either way, depending on which fragments map ambiguously:

| dataset | unique only | this PR |
|---|---|---|
| SRR13638690 muscle, 2×170 bp, selective alignment | 159.5 | 164.4 |
| SRR13638690 muscle, sketch | 163.9 | 168.1 |
| GEUVADIS ERR188044, 10M pairs, selective alignment | 172.8 | 170.1 |

For an ambiguous fragment, the shortest implied length is never longer than its true length. So when the mean rises, as on muscle, the unique-only sample was biased short by at least that much.

### Effect on abundances
The change is small, but where it is measurable it is an improvement. The table shows the change in transcript MARD against truth (this PR minus before), with a paired bootstrap 95% CI:

| simulation | selective alignment | sketch |
|---|---|---|
| GENCODE simA | **−0.00041** [−0.00072, −0.00007] | −0.00013 [−0.00039, +0.00014] |
| GENCODE simB | **−0.00034** [−0.00055, −0.00016] | **−0.00023** [−0.00045, −0.00002] |
| GENCODE simC | −0.00015 [−0.00039, +0.00007] | −0.00004 [−0.00029, +0.00024] |
| Ensembl r4m | −0.00006 [−0.00024, +0.00014] | −0.00005 [−0.00023, +0.00009] |

- Gene-level MARD improves on all six GENCODE runs, significantly on simB (both modes) and simC selective alignment.
- Gene-level Spearman rises slightly on simC and is unchanged elsewhere.
- The one change in the other direction is r4m sketch transcript L1/N: +0.00014 [+0.00000, +0.00029].

### Runtime
The FLD work itself is negligible. In a 1-thread `perf` profile of muscle sketch mapping, `record_discrete` goes from 0.60% to 0.79% of samples, about 0.07 s for 4.4M fragments. In the mapping pass each worker tallies into its own `LocalFld`, merged at thread end, so the extra lengths don't contend on shared atomics.

End to end, the two builds differ by a few tenths of a second, for two reasons unrelated to the FLD work.

**Code alignment.** With the default build, sketch mode looked up to 2% slower. Most of that is piscem-rs's `collect_live_targets`. The PR doesn't change it, and its machine code is identical in both builds; it just starts at a different 64-byte offset. Built with `-C llvm-args=-align-all-functions=6`, so both builds place it the same way:

| wall s (median of 3) | develop | this PR |
|---|---|---|
| muscle sketch, 1 thread | 38.22 | 38.59 |
| muscle sketch, 8 threads | 5.51 | 5.51 |
| GEUVADIS selective alignment, 8 threads | 24.43 | 24.55 |
| `--rad` with `--fldPolicy derive`, 4M pairs, 8 threads | 0.55 | 0.56 |

Forcing that alignment also moves develop's own 1-thread sketch time from 37.45 to 38.22 s.

**EM convergence.** GEUVADIS's remaining +0.1 s is in the EM. Under the new FLD, one slow-mixing component takes 6,968 iterations instead of 4,179. On muscle the iteration counts are identical. This depends on the data and could go either way on another sample.

### Testing
- `cargo test --release --workspace`: 384 passed. A new unit test checks that:
  - the shortest length wins;
  - ties go to the lowest transcript id, in either placement order;
  - ambiguous fragments don't count towards library-format detection;
  - a merged per-thread `LocalFld` equals direct accumulation.
- Clippy and rustfmt are clean.
- The per-thread build's `quant.sf` is byte-identical to the shared-atomic build's: muscle sketch, muscle selective alignment, GEUVADIS, and RAD re-derive.
- This branch's quant.sf is byte-identical to the experiment build used for the numbers above: r4m in both modes, and simA in selective alignment.
- Baked and re-derived FLDs agree. A map-only `--writeRad` run, quantified with the baked FLD and with `--fldPolicy derive`, gives identical `quant.sf`, matching the direct run (mean 180.342 in all three).

This changes estimates, so it belongs in the next minor release's notes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5e6b278c9ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
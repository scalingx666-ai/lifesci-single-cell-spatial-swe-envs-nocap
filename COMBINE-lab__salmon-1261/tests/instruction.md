# Issue

**Title:** perf: faster VBEM and selective alignment, lower peak memory

## Description

Speeds up inference and selective alignment and lowers peak memory. `quant.sf` stays byte-identical to `develop` in every check below.

> **Maintainer edits (Nov 1):**
> - merged `develop` and retargeted the PR to `develop`;
> - removed the `refseq.bin` memory mapping (salmon reads its index onto the heap, so a run's memory doesn't depend on the machine's memory pressure, and nothing is loaded lazily);
> - made the orphan skip reuse the pair alignments it computes;
> - wrote a frozen VBEM component's reduced layout over its own incidences instead of into a copy, which removes most of the extra memory the freeze cost with bootstraps.
>
> This PR includes all of #1260 (the flank shortcut and `KSW_EZ_NO_MAX`), which it supersedes. x86 results are added below. Benjamin's original description follows, updated for these edits.

## Changes

**Inference**
- VBEM takes dead transcripts (`alpha + prior == prior`) out of the projected-stop loop. Their abundances are recovered from the class scales at each check, and they come back if a term stops being negligible.
- The transposed incidences are built per component and shrink with it.
- A component without its dead transcripts is laid out over the front of its own incidences, not copied. The dead members are read back from the source classes when they are checked, and the component is laid out whole again at the end.
- The collapsed eq-classes are freed once packed when no bias correction will read them.

**Selective alignment**
- A read flank is settled from its ungapped alignment where the scoring proves no gap can beat it, and otherwise the DP gets less of the reference. Soft-clipping and ambiguous bases on the diagonal still go to the full DP.
- Flanks run last and stop once the read cannot reach the acceptance threshold, which also narrows their DP band. The cache holds rejections alongside exact scores.
- Flank and gap DPs pass `KSW_EZ_NO_MAX` (ksw2rs 0.2.1, COMBINE-lab/ksw2rs#2).
- The reverse complement of a read is kept between candidates.
- Orphans are skipped when a valid joint pair exists, except under `--recoverOrphans`. The pairs aligned for that check are reused instead of aligned again.

## Results

### x86 (AMD EPYC 9575F, pinned cores, Linux), selective alignment, wall seconds at 8 threads
Medians of 3–4 alternating runs. Each column adds to the previous; "#1261" is this PR's alignment changes without the edits above.

| | develop | #1260 | #1261 | this PR |
|---|---|---|---|---|
| SRR13638690 muscle, GENCODE v50, 4.4M pairs | 20.76 | 15.40 | 15.00 | 14.87 |
| GEUVADIS ERR188044, Ensembl, 10M pairs | 24.38 | 20.23 | 17.61 | 17.50 |

What each alignment change is worth on GEUVADIS:
- orphan skip: about 1.6 s;
- early stop at the threshold: about 0.4 s;
- trimmed flank reference and reverse-complement memo: about 0.5 s;
- reusing the pair alignments: about 0.1 s.

On muscle the changes on top of #1260 are worth about 3%.

VBEM time (`quant --rad`, seconds):

| RAD | 1 thread, develop → this PR | 16 threads, develop → this PR |
|---|---|---|
| GEUVADIS | 9.79 → 6.52 | 1.30 → 1.02 |
| GENCODE simA | 3.92 → 2.05 | 0.69 → 0.58 |
| muscle | 0.88 → 0.70 | 0.14 → 0.09 |

On GEUVADIS's largest connected component (131k transcripts, 3.5M incidences), 43% of the incidences are dead by iteration 114, and none comes back.

### Memory
Without the mapping, the eq-class freeing lowers peak RSS by 5–10% in `--rad` mode (muscle at 1 thread 599 → 548 MB). Reads mode is unchanged, since the index sets the peak there.

With bootstraps, each replicate in flight runs its own EM. Before the in-place layout, the freeze gave each of them a reduced copy of its largest component. Measured on GEUVADIS with 20 bootstraps at 16 threads:

| | peak RSS | wall |
|---|---|---|
| without the freeze | 1.26 GB | 20.3 s |
| freeze, reduced copy | 1.73 GB | 13.3 s |
| freeze, in place (this PR) | 1.44 GB | 13.0 s |

The 0.18 GB that remains is the freeze's per-transcript state and class boundaries, about 8 MB per replicate.

### Apple Silicon (Benjamin's runs, before the edits)
v2.9.1 -> this PR, SA, `-p 16`, medians of 6 ABBA-ordered pairs, on a shared machine, wall and user CPU:
- muscle SRR13638690: 12.9 -> 9.3 s, 179 -> 128 s;
- mouse hypothalamus, 10M pairs: 16.9 -> 11.1 s, 205 -> 124 s.

His peak-footprint figures came mostly from the mapping and no longer apply.

## Verification
- `cargo test --release --workspace`: 388 passed. Clippy and fmt are clean.
- The in-place layout gives the same `quant.sf` as the reduced copy on GENCODE simA with:
  - the default VBEM, `--useEM` and `--perNucleotidePrior`;
  - `--vbPrior` 1 and 1e-5, and `--stopRule global`;
  - Gibbs and bootstrap samples, which are also identical;
  - 1 and 16 threads.
- On GEUVADIS it gives the same bootstraps and point estimate. A unit test checks that `run` leaves the plan whole.
- `quant.sf`, the sorted `--writeMappings` SAM, and the `meta_info.json` counters are identical to `develop` on 500k muscle pairs with:
  - the default options;
  - `--softclip`, `--softclipOverhangs`, `--recoverOrphans`;
  - `--fullLengthAlignment`, `--minScoreFraction 0.8`, `--hardFilter`;
  - single-end reads.
- `quant.sf` is identical on the full muscle and GEUVADIS runs, and so is `bootstraps.gz`.
- The inference changes were also identical on four RADs at 1 and 16 threads, with:
  - `--useEM`, `--perNucleotidePrior`;
  - `--vbPrior` 1, 1e-3 and 1e-5;
  - `--stopRule global`;
  - 20 bootstraps and 20 Gibbs samples;
  - `--seqBias --gcBias`.
- This identity is observed, not guaranteed: dropping the dead terms could change a rounding on other data.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6ecfc5fccb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
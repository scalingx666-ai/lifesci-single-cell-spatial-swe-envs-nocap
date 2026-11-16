# Issue

**Title:** fix(align): honour soft-clipping when a read overhangs the transcript end

## Description

**What**

`ksw2_flank_extend` returned the full gap penalty whenever the reference flank was empty, that is, when a read's first or last MEM ends exactly at a transcript boundary. The soft-clip branches were never reached, so `--softclip` and `--softclipOverhangs` had no effect on the one overhang they exist to clip.

With either soft-clip mode on, an empty reference flank now scores 0. Without soft-clipping, behaviour is unchanged.

**Why it matters**

Short references whose reads routinely extend past the 3' end lose those reads below `--minScoreFraction`. Mature miRNAs with untemplated 3' A/U tails (isomiRs) are the clearest case: a 22 nt read with a 4 nt tail could not be rescued by any soft-clip flag (details and a reproducer in the issue).

**Tests**

* Extended `flank_softclip_recovers_read_overhang` with the empty-flank case: negative score without soft-clipping, 0 with `softclip_overhangs` (3' flank) and with `softclip` (5' flank).
* `cargo test --release -p salmon-map`: 75 passed, 0 failed.
* Reproducer from the issue, after the fix:

| run | mapped | miR-21-5p NumReads |
|---|---|---|
| no flag | 91.30 % (unchanged) | 100 |
| `--softclipOverhangs` | 100 % | 300 |
| `--softclip` | 100 % | 300 |

Not checked: the impact on standard bulk RNA-seq data, beyond the existing tests.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf7c8ef0af3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
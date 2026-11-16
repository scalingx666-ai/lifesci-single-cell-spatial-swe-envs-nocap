# Issue

**Title:** CheckM 1.2.9: performance improvements (results unchanged)

## Description

> [!NOTE]
> **This release only improves performance. Results are unchanged.**
> On the 128-genome validation set, every output file is identical to CheckM 1.2.8, including the summary tables, `lineage.ms`, per-genome statistics, gene calls and HMMER hits.

This PR builds on #423 (1.2.8) and targets the `1.2.8` branch, so the diff shows only the 1.2.9 changes. GitHub retargets it to `master` once #423 is merged.

## Changes
**Marker gene identification** (`markerGeneFinder.py`)
- The marker file (`lineage.ms`) is parsed once instead of once per bin. The old approach scaled quadratically: about 10 s per bin with 1,000 bins.
- Bins are grouped by marker set, and each group's HMM file is fetched and parsed once. The 1,000-genome test set has only 373 distinct marker sets.
  - The HMM files are no longer indexed with `hmmfetch --index`; that index was never used.
  - At most one HMM file per thread exists at a time, so temporary disk use stays bounded.
- Larger bins are processed first, to avoid a long tail at the end of a run.
- When bins are searched one per thread, `hmmsearch` runs in serial mode (`--cpu 0`). `--cpu 1` starts an extra reader thread and uses about 15% more CPU for identical output.

**Parsing**
- Marker sets in `lineage.ms` and in the reference data are parsed with a cached, dedicated parser instead of `eval()`.
  - Parsing `lineage.ms` for 1,000 bins drops from 12.5 s to 1 s.
  - File contents are no longer evaluated as Python code.
- The Pfam clan file is read once per process instead of once per bin for every parse. Other reference files are also read once.
- `lineage_set` builds a label-to-node lookup once, instead of searching the 12,483-node reference tree for every bin.
- HMMER tables are split with `str.split()` instead of a regex. The fields are identical (checked on 1.1 M lines), at about half the cost.
- HMMER results are parsed in parallel. `qa` now uses its `-t` option, which it previously ignored.

**pplacer**
- `--pplacer_threads` now defaults to `-t`, to a maximum of 64; pplacer doesn't run properly with more threads. The default was 1, so users who didn't set it placed bins on a single thread.
  - For 1,000 genomes, pplacer drops from about 110 min to about 5 min.
  - Explicit values above 64 are reduced to 64 with a warning.
  - The help text claimed memory grows linearly with threads. pplacer's worker processes share memory, and peak use was about 35 GB at 1 to 64 threads.
  - Placements are identical for any thread count.

**Other**
- The README badges are cached for less time. The PyPI badge was showing 1.2.5 after 1.2.7 was released.

## Validation
- I ran `lineage_wf` on 128 randomly selected GlobDB r232 MAGs (112 bacteria, 16 archaea) with 1.2.8 and with this branch. Both used `-t 64 --pplacer_threads 64`, HMMER 3.4, Prodigal 2.6.3 and pplacer 1.1.alpha20.
- All compared outputs are **identical**: `qa_results.tsv`, `qa_extended.tsv`, `lineage.ms`, `bin_stats.tree.tsv`, `bin_stats.analyze.tsv`, `bin_stats_ext.tsv`, `marker_gene_stats.tsv`, and every genome's `genes.faa`, `hmmer.tree.txt` and `hmmer.analyze.txt`.
- `qa -o 2` output is identical with 1 and 32 threads.
- The new `lineage.ms` parser gives the same result as `eval()` on all 45,302 marker-set strings in `lineage.ms` files from 1.2.7 and 1.2.8 and in the reference data.
- Unit tests: 156, all passing.

## Timing: 128 genomes, 64 threads (seconds)
| Stage | 1.2.8 | 1.2.9 |
|---|---|---|
| tree: marker search (Prodigal + `hmmsearch`) | 76 | 78 |
| pplacer | 221 | 226 |
| analyze: marker search (`hmmsearch`) | 200 | 193 |
| Python stages (`lineage_set`, parsing, `qa`, other) | 78 | 21 |
| **Total `lineage_wf`** | **575** | **518** |
| Separate `qa -o 2` | 22 | 6 |

**Where the gains are larger than this table shows:**
- **At 128 genomes, most of the remaining time is in the external programs:** pplacer (mostly a fixed setup of about 3 minutes), `hmmsearch` and Prodigal. Those are unchanged.
- **The Python stages are 73% faster.** Several of the removed costs grew quadratically or ran serially, so the saving should be much larger on bigger runs.
- **Default users gain the most.** Anyone who didn't set `--pplacer_threads` sees the biggest improvement from the new default.

This branch has not yet been run on the 1,000-genome set.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf468d20c682`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
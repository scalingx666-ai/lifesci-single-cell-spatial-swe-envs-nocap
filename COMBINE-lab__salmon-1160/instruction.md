# Issue

**Title:** fix: four release blockers found by the pre-2.6.0 readiness sweep

## Description

The readiness sweep you asked for found four defects that block a tag. **Three of them I introduced with the audit fixes**, which is the most useful thing this pass produced: each type-checked, passed the full suite, and still produced wrong or missing output on a default, non-deprecated path.

## B1 — `-g` was a total no-op in the default reads mode (mine, #1156)

The most common salmon invocation. `run_deterministic` takes the user's `--skipQuant` into `stop_after_mapping`, then forces `map_opts.skip_quant = true` for phase 1; my gene-level guard tested the **mutated** field, so `write_gene_level` became dead code. Sharper still: a genuine `--skipQuant` returns earlier, so the "gene-level aggregation skipped" explanation printed *only and always* on runs that never passed `--skipQuant`. Guard removed — reaching that point means phase 2 ran.

```
$ salmon quant -i idx -l IU -1 r1.fq -2 r2.fq -o out -p 2 -g t2g.tsv
 INFO --skipQuant: gene-level aggregation (-g) skipped — no abundances were estimated
$ ls out            # exit 0, no quant.genes.sf
```

## B2 — `--perNucleotidePrior` never reached bootstrap replicates (mine, #1158)

`run_em_counts` takes `init_alphas: Option<&[f64]>` immediately before `eff_lens: Option<&[f64]>`. I passed the effective lengths one slot early. Both are the same type, so it compiled silently — the prior stayed flat **and** every replicate warm-started from the effective-length vector. The reported posterior spread was drawn under a different prior than the point estimate it quantifies. `finalize_truncate_redistribute` had the same omission.

Verified on a contested eq class: replicate means now track their point estimates (204.1↔203.9 flat, 212.2↔212.1 per-nucleotide); before, both centred on the flat answer.

## B3 — `--recoverOrphans` inverted the strand when mate 2 anchored (mine, #1154)

The record already branched on `anchor_is_left` for `r1_pos`, `r2_pos` and `r1_score`, but took `is_fw`, `r2_fw` and `format` from the anchor unconditionally. The inversion **predates** #1154 — what my change did was feed that recorded format to the strand filter, turning a latent bug into one that silently zeroes stranded libraries. Mate strands are now derived once from `anchor_is_left` and used for all three, matching the proper-pair convention (`is_fw` = mate 1, `r2_fw` = mate 2).

With mate 1 too short to seed, so mate 2 anchors, on an ISF-by-construction library:

| | before | after |
|---|---|---|
| `-l ISF` (correct) | 0% mapped | **100% mapped** |
| `-l ISR` (wrong) | 100% mapped | **0% mapped** |

Note the one-pass/deterministic parity fix from batch C holds throughout — both paths agreed on the *wrong* answer, so cross-path diffing could never have caught this.

## B4 — an unsatisfiable `-p` aborted with a raw panic (pre-existing)

Exit 134, from a message that asserts the global pool both was and was not initialized and names neither `-p` nor the cause. The trigger is ordinary: an unset `$SLURM_CPUS_PER_TASK`, a typo'd digit — and the threshold scales with machine size. `-p` is now clamped to `available_parallelism()` with a warning naming both numbers, and `build_global()`'s error is propagated rather than discarded.

## Tests

All four are pinned end to end through the binary, because every one was invisible at the unit level. B2 is pinned in `salmon-infer` against a contested class over transcripts of differing effective length — the only shape where a per-nucleotide prior is distinguishable from a per-transcript one.

Suite **320 passed / 0 failed**, clippy clean.

The sweep's remaining findings (should-fix, mostly the reads-vs-`-a`/`--rad` applicability gap and some metadata fields that assert something false) are not in this PR; I'll summarize them separately so you can decide what lands before the tag.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f5e7f0a32fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
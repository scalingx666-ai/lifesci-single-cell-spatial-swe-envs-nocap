# Issue

**Title:** fix(genemap): read --geneMap before quantifying, and steer users to tximport

## Description

.

#1076 fixed the gzip half of that issue. This is the other half: *when* the annotation is read.

## The problem

Gene-level aggregation is the last thing a run does, and `write_gene_level` opened the annotation as its first action. So an unreadable `--geneMap` failed the run **after** mapping, inference and `quant.sf` had all completed. The exit is non-zero, so a pipeline treats the step as failed — with every expensive artifact already written.

Measured on the sample data before this change (log order is what matters; the run is far too quick for elapsed time to show it):

```
salmon_quant: mapped 10000 / 10000 fragments (100.00%)
salmon_quant: writing results to .../out_missing
salmon: processed 10000 fragments, mapped 10000 (100.00%), 27 equivalence classes
Error: reading gene map .../nope.gtf
  Caused by: No such file or directory (os error 2)
```

## The fix

The map is read and parsed during argument setup and carried on `GeneMapOpts`, so the failure lands before any work begins.

Parsing it rather than merely stat-ing it is deliberate: it also catches a malformed annotation, not just a missing file. The parse is *moved*, not added — the run needed it anyway — at the cost of holding the map for the duration, which is the same map the run would have held at the end.

| | before | after |
| --- | --- | --- |
| missing annotation | maps 10,000 fragments, writes `quant.sf`, then exits 1 | exits 1, **nothing mapped, no output directory** |
| malformed annotation | same | same as above |
| valid `.gtf.gz` | works | works, `quant.genes.sf` present |

## tximport notice

`--geneMap` now emits:

> tximport (R) and pytximport (Python) are the preferred way to obtain gene-level estimates from salmon output: they offer several ways to aggregate transcript abundances to the gene level, including one that computes an offset accounting for changes in average transcript length between samples. `--geneMap` may be removed in a future release.

The notice points at what tximport offers rather than characterising what `--geneMap` does not do — the length-offset method is one of several aggregation options there, and that is the reason to prefer it. Nothing is emitted when the option is unused (verified).

Documented in the CLI reference under a new *Prefer tximport for gene-level estimates* section, with the flag's table entry pointing at it.

## Also

The unmatched-transcript warning now names the annotation it failed to join against, which matters when several are in play. The `path` field would otherwise have become dead once the deferred read went away.

## Tests

One unit test on `load_gene_map`: absent option, missing path (error names the file), and a valid annotation parsed into the opts. Negative-controlled — restoring the deferred read makes it fail, so it pins the behaviour rather than passing vacuously.

`cargo fmt`, `clippy --workspace --all-targets -D warnings` and the full suite are clean. Touches only the CLI crate and the docs page.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e36857533b52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
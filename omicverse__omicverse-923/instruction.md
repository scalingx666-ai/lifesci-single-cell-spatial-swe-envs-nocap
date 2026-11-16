# Issue

**Title:** feat(airr): resolve 'multichain' into its biologically distinct subtypes

## Description

.

## The report is right

`chain_qc` put every cell with more than one chain in an arm into a single `multichain` bucket. So 2 TRA + 1 TRB, 1 TRA + 2 TRB and 2 TRA + 2 TRB were indistinguishable from genuine doublets, and the tutorial's `!= 'multichain'` filter threw all of them away. Dual TCRα expression is a documented consequence of incomplete allelic exclusion at the *TRA* locus — those are real T cells. Whether to keep them is a question about the biology under study, not something QC should decide unilaterally.

The module docstring claims `chain_qc` is "a clean reimplementation of scirpy's `tl.chain_qc`", but scirpy has always distinguished `extra VJ` / `extra VDJ` / `two full chains` from `multichain`. The reimplementation had dropped those categories.

## What changed

**1. scirpy's full vocabulary.** `chain_pairing` is now an ordered categorical over:

| category | configuration |
|---|---|
| `single pair` | 1 TRA + 1 TRB |
| `extra VJ` | **2 TRA + 1 TRB** — the dual-α case from the issue |
| `extra VDJ` | **1 TRA + 2 TRB** |
| `two full chains` | **2 TRA + 2 TRB** |
| `orphan VJ` / `orphan VDJ` | only one arm recovered |
| `multichain` | more than two chains in one arm — chains were dropped |
| `ambiguous` | loci that form no known receptor (TRA + IGH) |
| `no IR` | nothing |

**2. The reader now records what it drops.** This is what makes the split safe. `_contigs_to_cells` keeps the top two chains per arm by `duplicate_count` and silently discarded the rest — after truncation a 3-TRA cell looks exactly like a 2-TRA cell. It now writes `obs['multi_chain']`, and `chain_qc` reserves `multichain` for those cells. Without this, the new granularity would quietly relabel real doublets as `extra VJ`. All five readers funnel through `_contigs_to_cells`, so they all gain it; `chain_qc` tolerates its absence so old h5ad files still classify.

**3. `ov.airr.filter_chains(adata, keep=...)`** — the "selectively retain" part of the ask, as one argument instead of a hand-built mask:

```python
ov.airr.chain_qc(adata)
tcr = ov.airr.filter_chains(adata, keep='strict')   # single pair only (previous behaviour)
tcr = ov.airr.filter_chains(adata, keep='paired')   # + dual-receptor cells
tcr = ov.airr.filter_chains(adata, keep='any IR')   # everything with a receptor
tcr = ov.airr.filter_chains(adata, keep=['single pair', 'extra VJ'])
```

## Two bugs surfaced on the way

- A cell with **unmatched loci (TRA + IGH) was reported as `single pair`** — one VJ chain and one VDJ chain, so the count-based logic saw a clean pair. It is now `ambiguous`, matching scirpy.
- A cell with **two VJ chains and no VDJ was `multichain`**; scirpy calls it `orphan VJ`, and so do we now.

`_classify_cell` also contained a dead first `if/elif` block whose result was overwritten by the block immediately below it (including an unreachable `"extra chain"` branch). Removed.

## Verification

**Against scirpy, on identical input** — one 10x contig CSV covering 13 configurations, read and classified by both stacks:

```
        config       omicverse          scirpy  n  match
     ambiguous       ambiguous       ambiguous  3   True
      bcr_pair     single pair     single pair  3   True
     extra_vdj       extra VDJ       extra VDJ  3   True
      extra_vj        extra VJ        extra VJ  3   True
       gd_pair     single pair     single pair  3   True
     multi_vdj      multichain      multichain  3   True
      multi_vj      multichain      multichain  3   True
    orphan_vdj      orphan VDJ      orphan VDJ  3   True
orphan_vdj_two      orphan VDJ      orphan VDJ  3   True
     orphan_vj       orphan VJ       orphan VJ  3   True
 orphan_vj_two       orphan VJ       orphan VJ  3   True
   single_pair     single pair     single pair  3   True
      two_full two full chains two full chains  3   True

cells compared : 39      label agreement: 100.0%
```

**Against `master`, same cells** — 18 of 39 labels change, and every change is one of the four defects:

```
        config      master         this PR
     extra_vdj  multichain       extra VDJ     <- was discarded
      extra_vj  multichain        extra VJ     <- was discarded (the issue)
      two_full  multichain two full chains     <- was discarded
orphan_vdj_two  multichain      orphan VDJ     <- wrong bucket
 orphan_vj_two  multichain       orphan VJ     <- wrong bucket
     ambiguous single pair       ambiguous     <- silently wrong
     multi_vdj  multichain      multichain     <- correctly unchanged
      multi_vj  multichain      multichain     <- correctly unchanged
```

The last two rows are the ones that matter for safety: true >2-chain cells stay `multichain`, which only works because of the reader flag.

**Tests** — `tests/airr/test_chain_qc.py`, 24 new tests covering every category, the presets, error paths, the missing-`multi_chain` fallback, and the reader keeping the highest-UMI chains. `pytest tests/airr` → **32 passed**.

Nothing else in the codebase reads `chain_pairing`, so no downstream behaviour changes silently.

Tutorial update to follow in omicverse-tutorials.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VVqVNig3oV6wz42YiQ9obZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc7761ab5781`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
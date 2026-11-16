# Issue

**Title:** fix(bulk): TMM-normalize library sizes before voom in the limma paths

## Description

.

## Root cause
`deg_analysis(method='limma')`, `continuous_deg` and `timecourse_deg` (count input) called `_limma.voom(counts, design)` on raw column sums and never ran `calcNormFactors`. The standard limma-voom workflow is `DGEList → calcNormFactors (TMM) → voom(lib.size × norm.factors)`. Without TMM, a group with a block of strongly up-regulated genes gets a larger library, so every unchanged gene's logCPM drops and many come out as significant. pylimma itself is fine: given TMM library sizes it is calibrated.

## Fix
- New private helper `_tmm_lib_sizes(counts)`: `effective_lib_sizes(calcNormFactors(DGEList(counts)))` using the vendored pyedger, the same TMM the `edger` / `edgepy` branches already use.
- All five `voom` calls now get `lib_size=`:
  - `deg_analysis` limma
  - `continuous_deg`
  - `timecourse_deg`: the plain call and both rounds of the repeated-measures (`block`) path
- The `'continuous'` paths (no voom) are unchanged.
- Docstrings say "voom on TMM library sizes".

**Behaviour change:** limma / `continuous_deg` / `timecourse_deg` results on count input change wherever the TMM factors differ from 1. This is worth a line in the release notes.

## Numbers
The #994 example (2000 genes, 4 vs 4 Poisson, genes 0–99 4× up), `method='limma'`:

| | unchanged genes at q < 0.05 (of 1900) | unchanged genes at p < 0.05 (≈95 expected) | median log2FC of unchanged genes | planted found |
|---|---|---|---|---|
| master 976a4f57 | 1409 | 1449 | −0.211 | 100/100 |
| this PR | 4 | 101 | −0.008 | 100/100 |

## Tests
Two tests in `tests/bulk/test_deg_backends.py` use Poisson counts where 50 of 1000 genes inflate some libraries by ~15%:

| test | master | this PR |
|---|---|---|
| `test_limma_unchanged_genes_not_shifted_by_composition` (4 vs 4, genes 0–49 4× up) | **fails**: 72% of unchanged genes at q < 0.05, median log2FC −0.22 | passes: 0%, −0.01; all 50 planted `up` |
| `test_continuous_deg_unchanged_genes_not_shifted_by_composition` (genes 0–49 scale with a 0–3 trait) | **fails**: 34%, median slope −0.062 | passes: 0.1%, −0.004; all 50 planted significant |

Each new test takes < 1 s.

Run on Linux x86_64 / CPython 3.11.17:
- `tests/bulk/test_deg_backends.py` + `tests/bulk/test_timecourse_deg.py`: 39 passed, 1 skipped (the existing `pymfuzz` skip, which also skips on master).
- The timecourse tests pass 17/17 both before and after. The comment on their fixture size now mentions TMM.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `976a4f570f2a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
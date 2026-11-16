# Issue

**Title:** deps: use pyedger from PyPI instead of the vendored copy

## Description

## Summary
- `pyDEG.deg_analysis(method="edger"/"edgepy")` and `Milo.da_nhoods` now `import pyedger` (PyPI, [omicverse/py-edgeR](https://github.com/omicverse/py-edgeR)) instead of the vendored copy in `omicverse/external/pyedger`.
- New dependency: `pyedger>=0.2.0`.
- The vendored 0.1.0 copy (`core.py`, 2.2k lines) is removed. `omicverse.external.pyedger` stays importable as an alias that resolves to the installed package.

## Why
The vendored copy was pyedger 0.1.0. That version only matched edgeR on the two-group path, and with a design matrix it took hours on ~1e5 features.

pyedger 0.2.0:
- tracks **edgeR 4.10.5 / limma 3.68.5**, the current Bioconductor release. This includes the new QL method, which is the default (`legacy=FALSE`), and limma's `fitFDistUnequalDF1`;
- has vectorised GLM kernels (about a minute on ~1e5 features);
- fixes NaN tagwise dispersions when `prior.df = Inf`. Without that fix, `method="edgepy"` returned an empty table on low-dispersion data; `test_backend_schema_and_recovery[edgepy]` catches this.

**Behaviour change:** `method="edger"` and Milo already called `glmQLFit(legacy=False)`. They now get edgeR 4.4+'s version of that method instead of 0.1.0's approximation, so p-values change and follow current Bioconductor edgeR.

## Milo parity test
The reference (`milo_edger_reference.csv`, edgeR 4.4.0) now matches to about 2e-9 in F and PValue, and about 1e-13 in logFC. The test therefore compares logFC, F and PValue at rtol 1e-6. Before, it checked F Pearson > 0.99 and PValue Spearman > 0.99.

## Tests
With pyedger 0.2.0 from PyPI:
- `tests/bulk/test_deg_backends.py` and `test_milo_pyedger_matches_bioconductor_edger`: 17 passed.
- `test_milo_da_nhoods_runs_without_inmoose` aborts in my local env while importing tensorflow under the import hook. It aborts the same way on unmodified master, so it is environment-related.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01SrHqTobj75EpUfD2Pn1hg6

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13b88d589d13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
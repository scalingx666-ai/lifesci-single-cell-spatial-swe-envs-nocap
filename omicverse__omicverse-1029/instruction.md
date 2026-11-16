# Issue

**Title:** deps: use python-limma from PyPI instead of the vendored pylimma

## Description

## Summary
Same change as #986 for pyedger, now for limma.

- `omicverse/external/pylimma/` no longer vendors the code: `__init__.py` is an alias (`sys.modules[__name__] = pylimma`), so `from ..external import pylimma` keeps working and resolves to the installed package; `fit.py` and the copied LICENSE are removed.
- `pyproject.toml`: new dependency `python-limma>=0.1.1` (PyPI name; the import name is `pylimma`).
- Comments/docstrings in `bulk/_Deseq2.py` and the two test modules no longer say "vendored" (also the stale one on the pyedger path).

## Why
python-limma 0.1.1 () is R-parity tested against limma 3.68.5: identical DE calls on eight TCGA tumour–normal cohorts and 60 small-sample draws, P-values within 1.6e-4 (median 2e-10). It includes the moderated-t fix the vendored copy already had (`stdev.coef.lim` applied only to the B-statistic, #927) and adds the B-statistic and `lmFit(EList)`. Report: omicverse/omicverse-org-home#32.

## Compatibility
Every call omicverse makes is unchanged in 0.1.1: `voom` (incl. `block`/`correlation`), `lmFit` (weights, block, correlation), `contrasts_fit`, `duplicateCorrelation`, `eBayes(fit)`, and the fields read from the fit (`coefficients`, `t`, `p_value`, `Amean`, `df_total`, `cov_coefficients`). `topTable`'s new default sort (by B) does not matter here — omicverse does not call it. No other module imports pylimma (`ov.protein` and `ov.metabol` use their own limma code).

## Tests
`tests/bulk/test_deg_backends.py` and `tests/bulk/test_timecourse_deg.py` with python-limma 0.1.1 and pyedger 0.2.3: 39 passed, 1 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e91fa7bee000`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
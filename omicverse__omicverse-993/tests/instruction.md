# Issue

**Title:** fix(bulk): import pydeseq2 only in the DEseq2 branch of pyDEG.deg_analysis

## Description

.

## Root cause
`pyDEG.deg_analysis` imported `pydeseq2.dds` / `pydeseq2.ds` at the top of the function, before branching on `method`. pydeseq2 is only in the `full` / `easy` / `tests` extras, so on a plain install `ttest`, `edger`, `edgepy` and `limma` all raised `ModuleNotFoundError: No module named 'pydeseq2'`, although none of them uses it.

## Fix
- Move the pydeseq2 imports into the `DEseq2` branch, wrapped in `try/except ImportError`.
- The error message is in the same style as `ov.micro`'s `DA.deseq2`: `method='DEseq2' requires pydeseq2 (pip install pydeseq2). method='edger', 'edgepy', 'limma' and 'ttest' do not need it.`
- No behaviour change when pydeseq2 is installed.

## Tests
`tests/bulk/test_deg_backends.py`, with a `no_pydeseq2` fixture (`monkeypatch.setitem(sys.modules, "pydeseq2", None)`):
- `test_methods_run_without_pydeseq2[limma|edgepy|ttest]`: returns a result.
- `test_deseq2_without_pydeseq2_raises_install_hint`: `ImportError` matching `pip install pydeseq2`.
- `edger` is left out of the parametrization only for speed (~57 s on the 400-gene fixture). It takes the same pre-branch code path, and the existing tests still exercise it with pydeseq2 installed.

Run on Linux x86_64 / CPython 3.11.17 with pydeseq2 0.5.1:
- On master d25a9a9a the 5 new tests (edger was still in at that point) **all fail** with `ModuleNotFoundError ... _Deseq2.py:631`.
- On this branch the whole file passes (21 passed with the edger case, 141 s). After dropping edger, the new tests pass in 19 s.

Related, not in this PR:
- The version checks compare strings (`pydeseq2.__version__ <= '0.4.1'`), which would break on a two-digit minor such as `0.10.0`.
- pydeseq2 ≥ 0.5 warns `design_factors is deprecated and will soon be removed`; the branch could pass `design="~condition"` instead.
- The `limma` branch's missing TMM normalization is tracked separately in #994.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d25a9a9afb09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
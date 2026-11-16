# Issue

**Title:** fix(synbio): drop rs3 from the [synbio] extra — it made the extra uninstallable

## Description

## The bug

`pip install "omicverse[synbio]"` has **never worked**. It fails with `ResolutionImpossible` on every Python version, under both pip and uv:

```
The conflict is caused by:
    omicverse 2.2.4 depends on scikit-learn>=1.2
    rs3 0.0.18 depends on scikit-learn<=1.0.2 and >=0.24.2
ERROR: ResolutionImpossible
```

`rs3 0.0.18` is the **only** release satisfying `rs3>=0.0.18`, so no resolver can back off. One unsatisfiable requirement took the entire extra down with it — none of the other 19 dependencies (`cobra`, `dnachisel`, `straindesign`, `fair-esm`, `ViennaRNA`, `sbol2`, `rdkit`, …) could be installed either, so **no `ov.synbio` function had a working install path**.

`git log -S rs3 -- pyproject.toml` shows the pin arrived in #887, the initial commit of the module — this has been broken for the module's entire lifetime.

## Why nobody noticed

`ov.synbio` has no pytest coverage. The two existing scripts — `tests/synbio_coupling_demo.py` and `tests/synbio_gpu_smoke.py` — are not named `test_*.py`, and `[tool.pytest.ini_options] python_files = ["test_*.py"]`, so pytest never collected them. CI never installs `[synbio]` either.

## The fix

Drop `rs3>=0.0.18` from the extra, with a comment explaining why it must not come back.

`design_grnas(method='rs3')` already lazy-imported rs3 behind a `try/except`, so the function keeps working — but the old error message told users to `pip install rs3 sglearn 'lightgbm==3.3.5'`, which is **actively harmful**: in an omicverse env that downgrades scikit-learn to 1.0.2 and breaks omicverse (on macOS it fails outright, trying to build scikit-learn 1.0.2 from source — `clang: error: unsupported option '-fopenmp'`). The message now names the conflict, points at a separate environment, and offers `method='heuristic'` (the default, dependency-free) as the in-place alternative.

## Verification

Resolution after the fix, via `uv pip compile` against the real extra:

| Python | before | after |
|---|---|---|
| 3.10 | `No solution found` | Resolved **187** packages |
| 3.11 | `No solution found` | Resolved **184** packages |
| 3.12 | `No solution found` | Resolved **186** packages |

New `tests/test_synbio_crispr.py` (4 passed) — the first pytest-collected tests for `ov.synbio`:
- the default heuristic path works with **zero** optional dependencies
- unknown `method=` still raises `ValueError`
- `method='rs3'` raises an `ImportError` that names the `scikit-learn<=1.0.2` pin, offers the fallback, and points at a separate env (rs3 import blocked via monkeypatch so it holds on machines that do have rs3)
- regression guard: `rs3` is absent from the `synbio` extra in `pyproject.toml`

`tests/architecture/` is unchanged by this PR: `test_pl_canonical_aliases.py` fails identically on `master` (verified before/after).

## Not in this PR

- CI that actually installs `[synbio]` and runs a smoke test — the real reason this went unseen. Worth a follow-up.
- The tutorial `t_synbio_03_crispr_library.ipynb` (in the `omicverse_guide` submodule) calls `method='rs3'` with no note that it needs a separate environment. Needs a matching PR in the tutorials repo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1c381e202ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
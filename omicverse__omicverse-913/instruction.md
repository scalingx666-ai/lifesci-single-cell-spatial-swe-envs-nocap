# Issue

**Title:** feat(synbio): bring Rule Set 3 back via a --no-deps runtime fetch

## Description

, which had to drop `rs3` from the `[synbio]` extra to make the extra installable at all. That left `design_grnas(method='rs3')` reachable only by hand-building a separate environment. This brings it back properly.

## The pins were stale, not real

`rs3` pins `scikit-learn<=1.0.2`, `numpy<=1.26.4`, `lightgbm<=3.3.5`. But `RuleSet3.pkl` unpickles to a plain `lightgbm.sklearn.LGBMRegressor` — **there is no scikit-learn estimator in it at all**; scikit-learn is only lightgbm's own dependency. So I ran identical 30-mers through both stacks:

| stack | numpy / scikit-learn / lightgbm / pandas | `predict_seq` |
|---|---|---|
| rs3's own pins | 1.26.4 / **1.0.2** / **3.3.5** / 1.5.3 | `-0.11693749033657669` |
| modern | **2.4.6** / **1.9.0** / **4.7.0** / **3.0.5** | `-0.11693749033657669` |

Bit-identical.

## Approach

`omicverse/synbio/_rs3.py` installs `rs3` + `sglearn` with `--no-deps` into `$OMICOS_SYNBIO_WEIGHTS/rs3` (~20 MB, mostly the 17 MB `RuleSet3.pkl`) on first use — the same runtime-fetch pattern ProteinMPNN / CLEAN / DLKcat / PrimeDesign / LinearDesign already use — and lets the host env supply modern lightgbm/pandas/joblib.

`--no-deps` is the load-bearing flag: a plain `pip install rs3` into an omicverse env downgrades scikit-learn to 1.0.2 and breaks omicverse. Vendoring into `synbio/external/` was the alternative but would add 17 MB to every wheel and put a third-party Apache-2.0 tree under maintenance; rs3 is fetched from PyPI at runtime, not redistributed.

Adds `lightgbm>=4.0` + `seqfold>=0.7.7` to the extra — with `--no-deps`, nothing else pulls them in. `rs3` itself stays out, still guarded by a test.

## Two bugs only a real run surfaced

Both are now regression-tested. Neither was reachable from mocked tests.

1. **uv-built venvs have no pip.** `python -m pip` died with `No module named pip` — and that is exactly how the omicOS kernel env is built. uv is now the fallback installer; both commands are asserted to carry `--no-deps`.
2. **The pickle predates lightgbm 4.x.** `predict()` hit `'>' not supported between instances of 'NoneType' and 'int'` — 3.x had no `_n_classes`. Repaired on load (1 for a regressor), leaving a healthy value alone.

Also worth recording: do **not** reorder feature columns by `booster_.feature_name()`. lightgbm normalises `"Hsu2013 tracr"` to `"Hsu2013_tracr"`, so reindexing raises `KeyError`. The featuriser's own column order *is* the training order. I hit this while exploring and nearly shipped it.

## Verification

Full end-to-end on a clean weights dir, no mocks:

```
host python has pip? NO — so this exercises the uv fallback
design_grnas(method='rs3'): 1.3s, 5 guides
  GCTAGCTAGGATCCATCGAT CGG  rs3=-0.131428
installed: ['rs3', 'rs3-0.0.18.dist-info', 'sglearn', 'sglearn-1.2.5.dist-info']
cross-check vs rs3's own pinned stack: identical: True
```

- second call reinstalls nothing (0 installer invocations, cached)
- the pip path works too (verified in a pip-equipped venv)
- **host env untouched after a full run**: scikit-learn 1.7.2 / numpy 2.2.6, no downgrade
- extra resolves: **189 / 186 / 188** packages on 3.10 / 3.12 / 3.11
- `tests/test_synbio_crispr.py`: **10 passed**

## Pre-existing issue this makes visible (not fixed here)

`_score_rs3` only re-scores guides that have a full 30-mer context; the rest keep their heuristic score. Those two scores are different quantities — heuristic is 0..1, rs3 is a z-score — and `design_grnas` then sorts the mixed list by `efficiency`, so a heuristic 0.91 outranks an rs3 0.25 meaninglessly. Visible in the run above. This predates both PRs and needs its own decision (separate field? refuse to mix? pad the context?), so I left it alone.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `839835f1e7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
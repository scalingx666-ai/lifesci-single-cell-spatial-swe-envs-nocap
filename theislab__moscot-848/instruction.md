# Issue

**Title:** ci: unbreak the lint jobs (mypy python_version, dead doc links)

## Description

Both legs of the `Lint` workflow have been failing on `main` since **2026-07-27**, at the same SHA and for reasons unrelated to any code change — the last green run was 2026-07-06. Neither failure is caused by moscot code. The `Test` workflow is separately red on 3.12 (see below).

## `Lint code`

The `mypy` hook aborts inside numpy's own stubs:

```
numpy/__init__.pyi:737:45: error: Type statement is only supported in Python 3.12 and greater  [syntax]
Found 1 error in 1 file (errors prevented further checking)
```

numpy's stubs now use PEP 695 (`type X = …`), which needs `python_version >= 3.12`, while `[tool.mypy]` still pins `python_version = "3.10"`. mypy therefore never reaches any moscot source — it has effectively not type-checked the project for a month.

- Bump to `python_version = "3.12"`. The project requires `>=3.11`, so this only means checking under 3.12 semantics; no supported interpreter is dropped.
- Drop `plugins = "numpy.typing.mypy_plugin"`, deprecated in NumPy 2.3 and slated for removal.

With mypy actually running again, five `type: ignore` comments are reported as unnecessary (`warn_unused_ignores = true`) — three in `__init__.py`, one in `base/cost.py` (only the `type-var` code was stale, `arg-type` is kept), one in `problems/time/_mixins.py`. They are removed, after checking `moscot.__version__`/`__author__` still resolve. `mypy src` is then **clean: no issues found in 50 source files**.

The hook's environment installs only `numpy` (`additional_dependencies: [numpy>=1.25.0]`), so this is exactly what CI checks. Running mypy in a fully populated environment surfaces ~140 further errors from third-party stubs; that is a separate discussion and this PR does not touch it.

## `Lint docs`

`lint-docs` builds with `SPHINXOPTS = -W -q --keep-going`, so anything that warns fails it. Two causes:

1. **Dead links.** `make linkcheck` reported two upstream 404s — `muon.atac.tl.lsi` and an openproblems dataset page — both from `600_tutorial_translation.ipynb`, which lives in the `docs/notebooks` submodule and so cannot be fixed here. They join the existing `linkcheck_ignore` list, in its established commented style.
2. **Nine broken references.** Every remaining warning was `py:func reference target not found: scanpy.read`. These come from dataset docstrings saying "Keyword arguments for :func:`scanpy.read`" — but `_load_dataset_from_url` forwards `**kwargs` to `anndata.read_h5ad` (or `mudata.read_h5mu`), never to `scanpy.read`, which scanpy also no longer documents. Retargeted to :func:`~anndata.io.read_h5ad`, which fixes a factual error in the docs as well as the build. (`pancreas_multiome` already documented the right functions and is untouched.)

After this, the job has no broken links and no warnings left to trip `-W`.

## Not fixed here

The `Test` workflow fails on **ubuntu-3.12 and macOS-3.12** with **27 failures** (3.11 passes) in `test_annotation_mapping` and `test_set_graph_xy`. Those are pre-existing and orthogonal to lint: this PR touches only mypy config, `linkcheck_ignore` and docstrings, and reproduces the identical 27 failures. I also reproduced them locally with and without an unrelated source change and got identical counts. Worth its own issue.

## Verification

- `mypy src` under the hook's exact dependency set (mypy 1.15.0 + numpy only): clean.
- `black`, `isort`, `ruff`, `rstcheck`, `doc8` and the remaining hooks: pass (`prettier` needs Node, which I don't have locally — untouched by this diff).
- `pytest tests/solvers tests/utils`: 56 passed.
- `anndata.io.read_h5ad` confirmed present in anndata's intersphinx inventory.

Split out of #846, which is blocked on the same red lint.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `915643e7d639`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
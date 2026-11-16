# Issue

**Title:** fix: drop the undeclared six import from the TraCeR reader

## Description

Found while fixing the same break in sbi-dev/sbi#2148; no scirpy issue filed for it.

`scirpy/io/_tracerlib/core.py` still does `import six` for ten `six.iteritems` calls. `six` is not declared in `pyproject.toml`; it only arrived transitively through matplotlib → python-dateutil. python-dateutil 4.0.0 (2026-11-01) dropped `six`, so on a fresh `pip install scirpy` today, `import scirpy` works but `ir.io.read_tracer` raises `Exception: Error loading TCR data from cell ...` wrapping `ModuleNotFoundError: No module named 'six'`. The `test` group still pulls `six` in through other deps, which is why CI did not notice.

This replaces `six.iteritems(d)` with `d.items()` and drops the import. No behaviour change.

Tested by uninstalling `six` from the dev env: `test_io.py::test_read_tracer` fails on `main` with the error above and passes with this change (`test_io.py`: 33 passed). `ruff check`/`ruff format --check` at the pinned v0.16.7 are clean.

- [x] CHANGELOG.md updated
- [x] Tests added (For bug fixes or new features) — the existing `test_read_tracer` covers it once `six` is absent
- [ ] Tutorial updated (if necessary) — n/a

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a82b79345332`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
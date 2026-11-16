# Issue

**Title:** ci: install the declared test group in the conda job

## Description

Stacked on #1371 — GitHub retargets this to `main` once that merges.

## Problem

The `PETSc / SLEPc + R` job hand-rolls its test dependencies in the workflow:

```yaml
pip install pytest pytest-cov pytest-mock pytest-timeout coverage igraph leidenalg pillow
```

Every other job installs the `test` dependency group from `pyproject.toml`, so the two drifted in both directions:

- **`leidenalg` is dead weight.** It appears exactly once in the repo — that line. `_cluster_X` pins `sc.tl.leiden(..., flavor="igraph")` and the plotting tests pass `clustering_kwargs={"flavor": "igraph"}`, so only `igraph` (already in the group) is ever needed. It was added in #1291 (Feb 2026).
- **`pytest-timeout` is missing from the group**, even though it is a real test dependency — the conda job runs `pytest --timeout=600`, and `hatch test -- --timeout=…` fails locally because the hatch envs don't have it.

## Changes

- Declare `pytest-timeout` in the `test` dependency group.
- Install that group in the conda job: `pip install -e '.[plot]' --group test` (pip on the runner is 26.2.1; `--group` needs ≥ 25.1).

This matches [cookiecutter-scverse](https://github.com/scverse/cookiecutter-scverse), whose test workflow installs declared groups only (`hatch env create` + `hatch run …:run-cov`) and never an ad-hoc package list.

Note the conda job now also gets `jax`, `moscot` and `scvelo` from the group, so the tests that currently skip there run under the PETSc/SLEPc + R stack too — more coverage, at the cost of a somewhat longer install.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab23d63a9488`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
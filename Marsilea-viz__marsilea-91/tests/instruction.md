# Issue

**Title:** Require legendkit>=0.4.1

## Description

## Why

legendkit **0.4.1** is the first release that contains the fix for #83 (legend rendering broken under matplotlib 3.11). `dependencies` currently lists bare `legendkit`, so nothing stops a solver from picking an older release and reintroducing that bug.

This is not hypothetical — it is happening on conda-forge right now, reported as . The legendkit feedstock is stuck publishing 0.3.4 (its recipe still requests `flit-core` as the build backend, fixed in ), so `conda install -c conda-forge marsilea` happily resolves legendkit to 0.3.4 and #83 comes back. pip/uv are unaffected because PyPI has 0.5.0.

## What

* `pyproject.toml`: `"legendkit"` → `"legendkit>=0.4.1"`
* `uv.lock`: regenerated with `uv lock` — legendkit 0.3.4 → 0.5.0, no other package changed

The matching `run` requirement for `marsilea-feedstock` will be bumped separately, once legendkit 0.5.0 is actually on the conda-forge channel (adding the bound before then would make marsilea unsolvable on conda).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7cf29a7edd1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
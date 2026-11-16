# Issue

**Title:** Publish wheels to PyPI alongside the sdist

## Description

## Summary

- Adds `pyproject.toml` declaring the `setuptools` build backend (required by modern `python -m build`)
- Adds `.github/workflows/publish.yml`: a workflow that triggers on each GitHub Release, builds both the sdist and a `py3-none-any` wheel via `python -m build`, and publishes both to PyPI using OIDC trusted publishing

## Why wheels?

Since vireoSNP is pure Python (no compiled extensions), `python -m build` produces a `py3-none-any` wheel with zero extra effort. Users `pip install vireoSNP` will get the wheel, which:
- installs faster (no build step)
- works on all platforms without a compiler
- is still a single universal file because there's nothing platform-specific

## Setup required on the PyPI side

To use OIDC trusted publishing (no API token stored as a secret), the maintainer needs to add a trusted publisher on PyPI:
1. Go to https://pypi.org/manage/project/vireoSNP/settings/publishing/
2. Add a publisher: **GitHub** → owner `single-cell-genetics`, repo `vireo`, workflow `publish.yml`, environment `pypi`

That's it — no secrets to rotate.

## Tested locally

```
$ python -m build
Successfully built vireosnp-0.5.9.tar.gz and vireosnp-0.5.9-py3-none-any.whl
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3654633f766`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
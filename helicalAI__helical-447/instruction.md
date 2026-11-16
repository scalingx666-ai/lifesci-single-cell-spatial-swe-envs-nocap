# Issue

**Title:** Release 3.1.5

## Description

Releases helical **3.1.5**. When CI on this PR passes, the `release` job tags `v3.1.5` and publishes it to PyPI.

## Changes since the last release

- **fix(deps):** cap `transformers` below 5.21. transformers 5.21.x rejects `sdpa` attention for Gemma2, which breaks C2S (#446)
- **fix(mapping):** query Ensembl BioMart over https without pybiomart (#443)
- **ci:** cancel in-progress workflow runs when a new push arrives on the same PR, in `main.yml` and `release.yml` (#446)
- **ci(dependabot):** target `main` for GitHub Actions updates (#446)
- **build(deps):** bump `pypa/gh-action-pypi-publish` to 1.14.3 (#446), `actions/create-github-app-token` to 3.3.0 (#444), `hydra-core` to 1.3.7 (#441), and `mkdocs-material` to 9.7.7 in `/docs` (#425)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_011MJDaZLrTAKqmdeY4w1upu

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fc0af45531f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
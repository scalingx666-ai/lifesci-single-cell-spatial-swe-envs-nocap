# Issue

**Title:** build: pin GitHub Actions to full commit SHAs

## Description

## What

Pins every GitHub Actions `uses:` reference in this repo's workflows to a full 40-character commit SHA (with a `# <version>` comment), and adds `.github/dependabot.yml`.

## Why

Mutable tags like `@v2` / `@release/v1` are labels the action owner can silently repoint to malicious code — a supply-chain attack vector (OWASP A08:2021/2025, CWE-1357, CWE-353), exploited in the real-world tj-actions and trivy-action compromises. Since CI here handles secrets and publishes to PyPI, this is rated HIGH. Pinning to an immutable SHA closes the hole; Dependabot (added here) still surfaces real updates as reviewable PRs — nothing auto-merges.

## Notes

- `actions/checkout` bumped `v2`→**v5** (Node24; runners confirmed on Node24), `actions/setup-python` at **v5**, `actions/upload-artifact` at **v4**, `pypa/gh-action-pypi-publish` pinned at **release/v1**.
- `.github/dependabot.yml` ignores major bumps so pins get patch/security PRs without surprise majors.
- Supersedes #381 (same fix, re-targeted from `release` to `main`).

Refs helicalAI/dashboard#1154

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01ECugizP29xGmLLDBDLNzCm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de8d29e4f68a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
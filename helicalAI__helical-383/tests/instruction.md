# Issue

**Title:** build: pin GitHub Actions to full commit SHAs

## Description

* build: pin GitHub Actions to full commit SHAs

Pin every `uses:` reference in the workflows to a full 40-char commit SHA and add .github/dependabot.yml.

Mutable action tags (e.g. @v4, @release/v1) can be silently repointed by the action owner, enabling supply-chain attacks (OWASP A08, CWE-1357 / CWE-353) -- as seen in the tj-actions / trivy-action compromises. Pinning to an immutable SHA removes that risk; the trailing `# <version>` comment keeps it readable and lets Dependabot open reviewable update PRs. Runners are confirmed on Node24, so actions were bumped to their latest majors (checkout v5, ecr-login v2.1.6, etc.).

Refs helicalAI/dashboard#1154

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3929832a8a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
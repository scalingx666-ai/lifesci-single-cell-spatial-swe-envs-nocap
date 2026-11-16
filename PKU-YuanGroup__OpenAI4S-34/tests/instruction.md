# Issue

**Title:** Fix PyPI publish: pin gh-action-pypi-publish by release ref, not commit SHA

## Description

## Problem

The `v0.1.0` release's **Publish to PyPI** job failed in 4s with:

```
Unable to find image 'ghcr.io/pypa/gh-action-pypi-publish:7f25271a4…'
docker: Error response from daemon: manifest unknown
```

`pypa/gh-action-pypi-publish` is a **Docker container action**. Its generated Dockerfile does `FROM ghcr.io/pypa/gh-action-pypi-publish:${action_ref}`, and PyPA publishes that image tagged by **release ref only** (`release/v1`, …), never by commit SHA. So the SHA pin (`@7f25271…`) resolved to a non-existent image tag — the pull failed **before the container, and therefore the trusted-publisher OIDC exchange, ever started**. (This means the trusted-publisher config itself was never exercised; the next attempt is its first real test.)

## Fix

Pin this one action to `@release/v1` — PyPA's documented, image-backed ref. Every other action in the workflow stays SHA-pinned; this is the only Docker container action and the only one that cannot be SHA-pinned. Rationale is in an inline comment so nobody "re-hardens" it back to a SHA and breaks publishing again.

## Note for the scorecard

This trips the "pin actions by SHA" heuristic for this single step. It is unavoidable for a Docker container action whose image is release-tagged; the alternative (SHA pin) is simply broken.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d4ea0e7a85f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
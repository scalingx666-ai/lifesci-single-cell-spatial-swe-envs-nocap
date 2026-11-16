# Issue

**Title:** ci(packages): publish the container image to ghcr on release, smoke-gated

## Description

## Summary

Adds `.github/workflows/publish-image.yml`: on release publication (or manual dispatch against an existing `v*` tag), verify the tag against both version declarations, build the image, prove it with the same `scripts/container_smoke.sh` gate PR CI runs, and push `ghcr.io/pku-yuangroup/openai4s:<version>` + `:latest` from the `ghcr` environment using the job's own `GITHUB_TOKEN`. linux/amd64 only for now — the science stack under QEMU multiplies build time; arm64 is a deliberate later addition. The workflows README pair documents the new file and its intro count moves from three files to four.

After merging, publishing the v0.2.0 release triggers it automatically (or dispatch it once against `v0.2.0`); the README's Docker section ('No image is published yet') gets updated in a follow-up once the package actually exists.

## Verification

Ran: `scripts/check_directory_readmes.py` (bilingual pair updated, gate green). Not run: the workflow itself — it needs a published release or a dispatch, which happens post-merge.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c5e80a38306e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
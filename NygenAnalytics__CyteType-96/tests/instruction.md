# Issue

**Title:** Unify API navigation and improve documentation discovery

## Description

Use the guide header and navigation throughout the Sphinx API reference while preserving API content, links and native search.

Publish API output once, exclude internal search pages from indexing, and provide consistent canonical URLs, page titles and logo preview metadata.

Validation: documentation tests, strict Sphinx and MyST builds, lint, and browser checks for navigation, themes and metadata passed.

Requires the updated shared assets from the documentation hub.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b62057601030`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
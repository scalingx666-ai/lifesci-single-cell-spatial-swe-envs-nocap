# Issue

**Title:** Change format of CHANGELOG to Markdown

## Description

This moves `CHANGELOG` to `CHANGELOG.md` and makes its format Markdown.

Plain text has a certain aesthetic appeal, but I've found it to be
self-defeating in the vast majority of cases. Most people are reading
the log from GitHub rather than through a local editor, and having real
links to pull requests and richer formatting available are very nice
features.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69c5afb5bd96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
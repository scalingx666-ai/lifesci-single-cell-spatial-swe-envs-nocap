# Issue

**Title:** Issue Template revamp

## Description

Inspired by @rharao's work on:
- 

This PR picks up where #9571 left off,  replacing our markdown issue templates with the newer [YAML forms](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms#about-yaml-syntax-for-issue-forms).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6885cfd30828`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** chore(dependabot): add PR assignees

## Description

## What
Add a team assignee list to the Dependabot config so update PRs are automatically assigned.

## Why
Assignees make sure these PRs aren't missed. (No Docker ecosystem block in this repo, so the patch-only base-image policy applied in the Docker-enabled repos doesn't apply here.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `240970a70c8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
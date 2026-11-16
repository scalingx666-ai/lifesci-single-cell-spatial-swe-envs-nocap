# Issue

**Title:** Fix Anthropic model naming formats for both direct API and OpenRouter…

## Description

… API. Update model names in documentation and code to use correct formats: direct Anthropic API uses date-suffixed models (claude-3-7-sonnet-20250219), while OpenRouter uses dot notation (anthropic/claude-3.7-sonnet). Also fix cluster ID validation to strictly require numeric IDs starting from 0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b58f4219ea62`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
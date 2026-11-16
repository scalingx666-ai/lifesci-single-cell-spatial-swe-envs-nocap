# Issue

**Title:** feat(skills): skill_browse_store — keyword/category lookup

## Description

Adds a precise-lookup counterpart to the semantic `skill_search_store`. `skill_browse_store(query=, category=)` hits `GET /api/store/packages` (exact keyword/category filter, no semantic ranking) — for when the agent knows a name/keyword or wants to browse a category. The prompt tells it which to use. Keyword search was never lost (it's also fused into `/recommend`); this gives the agent explicit choice. Unit-tested against staging (keyword 'docking'→18, category 'bioinformatics'→94). Draft.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94c02becb7ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
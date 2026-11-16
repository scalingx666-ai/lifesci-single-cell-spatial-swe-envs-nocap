# Issue

**Title:** fix(skills): proactive store discovery (search first, not fallback)

## Description

The store-search nudge was too soft ('if no local skill covers it') — agents just did non-trivial tasks themselves and never searched the store (verified live on staging: proteomics/clinical tasks, tools+guidance present, zero store search). Reworded SKILLS_GUIDANCE to make store search a default opening step for non-trivial tasks, even when the agent thinks it can do it unaided. Docker-validated: clinical-survival task now searches → adopts a store skill → completes → attempts rate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ab920f731d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
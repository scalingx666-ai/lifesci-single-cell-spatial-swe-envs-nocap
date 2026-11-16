# Issue

**Title:** Fix: stale references to renamed/moved code

## Description

After the modular refactor (#18) and the web visualizer (#19) several references in the docs and one user-facing error message went stale:

- docs/configuration.md: env var defaults referenced SIA_META_PROFILE / SIA_TARGET_PROFILE; the real names are SIA_META_AGENT_PROFILE / SIA_TARGET_AGENT_PROFILE (see sia/config.py).
- SECURITY.md: bypassPermissions section pointed at util.py, which is now a backward-compat shim; the option is in sia/agent_impls/claude.py.
- sia/web/server.py and the README/configuration docs suggested installing a 'sia-agent[web]' extra that does not exist in pyproject.toml - fastapi and uvicorn are already in the base dependencies, so the dashboard is always available.
- docs/architecture.md: directory tree still listed util.py as "Agent runner utilities" and pointed at META_AGENT_PROMPT / FEEDBACK_AGENT_PROMPT constants in orchestrator.py; the prompts now live in sia/prompts.py as build_meta_prompt / build_feedback_prompt, and the agent runners are under sia/agent_impls/.

No behavior change. ruff check and ruff format --check both pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01939270bcd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
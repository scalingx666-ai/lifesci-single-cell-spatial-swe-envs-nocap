# Issue

**Title:** feat(store): skill_publish tool — agents contribute skills back to the store (PR-2)

## Description

Adds `skill_publish(name, content, display_name?, description?, category?, derived_from?, derived_note?)` to the learning-system toolset → `POST /api/store/contribute` (store-scoped token, author = hosted user).

- Contribution starts **private**, auto-publishes only on reviewer **'recommended'**.
- **Lineage**: `derived_from` records the parent (shown in store + fed to the diff-aware reviewer); auto-captured from the most-recent `skill_adopt` when omitted.
- Handles 429 (cap) / 409 (dup, not-an-optimization) / 401/403 (login) with hints. Mirrors `skill_rate`. `py_compile` clean.

Pairs with pantheon-hub #31 (contribute backend) + #32 (diff-aware review).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0834c269fee9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
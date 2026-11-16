# Issue

**Title:** Add community health docs: Code of Conduct, Contributing, Governance, Roadmap

## Description

Adds the standard community-health and governance files the repo was missing:

- **CODE_OF_CONDUCT.md** — Contributor Covenant v2.1
- **CONTRIBUTING.md** — contribution guide, dev setup, PR process, and a policy for agent-authored contributions (reviewed and approved by a named human before merge)
- **GOVERNANCE.md** — roles, decision-making, and maintainers
- **ROADMAP.md** — project direction

Also allowlists these four files in `.gitignore`, which otherwise ignores root-level markdown except `README.md`.

These are linked from the OS4LS full application (Section 3 project-info fields) and support the project’s governance and sustainability story.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01KzzzExNk4ZpjjtLy3vZuNy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ff3bbcbc6cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
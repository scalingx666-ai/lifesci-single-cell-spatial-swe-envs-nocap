# Issue

**Title:** feat(cli): auto-open OA/proxy + interactive access prompts

## Description

This PR adds interactive access prompts and automation for Domain Research results in Pantheon-CLI.

Highlights
- Flags: `--access_open {oa|proxy|none}`, `--institution_proxy_url <template>`, `--save_proxy_url`.
- REPL UI: displays a table of `access_requests` and offers per-item actions; auto-opens OA or proxy links per mode.
- Persistence: proxy template optionally saved to `.pantheon_config.json` (prefs.institution_proxy_url).
- Docs: README updates for flags, env vars, and examples.
- Test utility: `scripts/test_cli_access_flow.py` for validating auto-open and prompts without network.

Files
- pantheon_cli/cli/core.py (flags + persistence)
- pantheon_cli/repl/ui.py (prompts + auto-open)
- README.md
- scripts/test_cli_access_flow.py

Notes
- Non-breaking: defaults to interactive prompts only when `access_requests` are present; auto-open is opt-in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af3624ef0a51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
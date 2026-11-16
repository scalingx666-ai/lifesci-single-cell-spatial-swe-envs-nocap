# Issue

**Title:** fix(endpoint): app upgrades become visible without an endpoint restart

## Description

Two stale-registry holes, surfaced by the first real h5ad→Vitessce open racing the dev sync:

1. **scan() never re-read manifests.** A same-dir known app kept its whole previous \`AppEntry\` — manifest included — to preserve live process state. An upgrade that added a backend stayed invisible until the endpoint restarted, regardless of how many \`app_registry\` rescans ran. Live state still carries over; the manifest now follows the file.
2. **call() rescanned only for unknown ids.** A known entry without a backend now also triggers one rescan before refusing.

Observed on staging: vitessce's manifest grew \`entry.backend\` via dev sync moments after the supervisor first scanned it; every subsequent \`app_call\` refused with \`app 'vitessce' declares no backend\` even though the file on disk declared one.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fec39f5a2663`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
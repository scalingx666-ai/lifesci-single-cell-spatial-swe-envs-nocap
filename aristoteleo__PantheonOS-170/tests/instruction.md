# Issue

**Title:** feat(endpoint): backends hot-reload when their source changes

## Description

A running backend kept the code it was spawned with; every dev sync or upgrade served stale behaviour until the 600s idle reap or a sandbox recreation intervened (observed three times today on staging: new \`example()\`/\`datasets()\` methods invisible, old reachability probes answering). #169 made the manifest follow the file — this makes the process follow the source.

- \`_AppProcess.code_stamp\` = newest \`.py\` mtime under the backend directory at spawn.
- \`call()\` compares disk vs process before dispatch; newer code retires the process (terminate → 5s → kill) and falls through to the normal spawn, whose fresh handshake also updates the method table.
- Not a crash: no backoff, no counter. Calls in flight postpone the restart.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b64406aff5e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
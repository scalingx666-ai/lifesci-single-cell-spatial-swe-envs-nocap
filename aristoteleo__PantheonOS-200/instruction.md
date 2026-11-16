# Issue

**Title:** boot: userspace env snapshot + deferred memory routing (PR-2)

## Description

Second round of cold-start cuts, following #199. Verified on a real Modal Volume with an in-sandbox NATS (boot → worker registered):

| | full evaluation | snapshot replay |
|---|---|---|
| userspace sourcing segment | 0.57 s (2–12 s on aged staging volumes) | **0.02 s** |
| whole boot → NATS registered | 3.82 s | **1.50 s** |

## What

1. **`pantheon-userspace.sh` snapshot fast path.** The full evaluation costs seconds on a network-backed volume (every stat/glob/mkdir is a round trip, plus interpreter spawns and a ~520 ms `micromamba activate`) — but its outcome is just exports and three shell functions. The full run now writes that outcome to a snapshot on the volume; later sourcings (the entrypoint and every pty that re-reads the file) replay one file instead. The snapshot's first lines guard its own validity: building/removing the analysis env flips a marker check, the replay fails, and sourcing falls through to the full evaluation — the documented "next shell discovers the new env" behaviour is kept intact. PATH entries are emitted as the same guarded prepends the live code uses. The entrypoint re-derives the snapshot in the background every boot; `PANTHEON_USERSPACE_REBUILD=1` forces the full path.

2. **ChatRoom memory routing deferred.** `set_search_dirs`/`set_active_dir` resolve+mkdir on the volume (~2 s of critical path on a real workspace) and none of it is needed before the NATS worker subscribes. Init moves to a daemon thread; readers that route by directory (`_dir_for_chat`, `new_memory`, `list_memory_metadata`) block on a routing event — bounded at 15 s, degrading to the home-only routing the old inline `try/except` already produced on failure.

3. `promote-agent.yml` post-promote note now points at the hub's `prewarm.yml` (Nanguage/pantheon-hub#56).

## Verified

- Probe sandbox on the staging image with the four files injected, real volume: numbers above; snapshot content has the validity guards and guarded PATH prepends; second boot logs the fast path; background routing completes with a `[STARTUP_PROFILE]` line.
- pty semantics through the snapshot: `conda is a function", `CONDA_PREFIX` points at the analysis env.
- `tests/test_template_manager.py` 5/5; the memory/chatroom/project test selection fails identically on the base branch (pre-existing, incl. a set of real-Gemini integration tests that un-skip via an env leak — byte-identical failures on both branches when run with the key).

Staging cold-boot projection with #199 + this: admin-type ~14 s → ~5 s; new-layout aged volumes ~40 s → ~8–10 s (remaining: container exec lag ~3 s + import ~2-3 s + endpoint ctor).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01MjLiwbbQ9h4iSKDpwUy9Jg

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cd6d3b99c7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
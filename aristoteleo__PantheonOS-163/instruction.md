# Issue

**Title:** refactor: run Python on a Jupyter kernel, and delete what that replaces

## Description

The toolset owned a small execution engine: a generator inside a loky worker, fed code over a pipe, with stdout and stderr redirected around each `exec`. It worked, but none of it was Pantheon's problem to solve — a Jupyter kernel is the same thing, specified, and this repo already had a toolset that drives one properly.

**Net effect: `python_interpreter.py` loses 285 lines, and `executor/` goes back to what it was.**

## Three things fall out rather than being written

**Other interpreters.** A kernel is chosen by kernelspec name and jupyter resolves it to whatever Python the spec points at, so code runs in the conda env on the Volume and a second env is a second spec. Reaching another interpreter previously meant moving `sys.executable` at the exact moment loky forked its worker — that whole mechanism is deleted, along with the measurement it took to get right. (On POSIX loky builds the child command line from `sys.executable` directly and consults neither its own `spawn.get_executable()` nor any env var; and it starts workers *lazily*, so patching around the constructor did nothing at all while appearing to work.)

**Figures.** matplotlib's inline backend publishes PNGs as `display_data`. The old path monkeypatched `plt.show` to write a file, stashed the path in a global, fetched that global with a second round trip, then read the file back. It is now one field of a message the kernel already sends.

**Crash recovery.** A dead kernel is a "session not found" reply; the mapping is dropped and the next call starts a fresh one. No restart-in-place path, and so no repeat of the bug where that path referred to `client_id` — a name that went away when interpreters were re-keyed per chat — and raised `NameError` instead of recovering, leaving the session broken for good.

## `result_var_name` is gone

Getting a value out was a second execution against a magic variable name. An agent that wants a value prints it, or leaves the expression on the last line, which is what `execute_result` is for. Its one programmatic user, the evolution evaluator, now prints marked JSON — the value crossed a process boundary as pickled bytes before and crosses it as text now, which for a dict of scores is the same thing.

## Behaviour change worth naming

A traceback is now a returned failure (`success: False`, traceback in `stderr`) rather than an exception raised out of the tool. For something an agent calls, the agent needs to read what went wrong. The test covers it.

## Verified on staging

```
run_python_code runs in   /workspace/.local/micromamba/envs/analysis
state persists            res=2 → res+1=3
stdout                    captured
error                     success=False, with traceback
figure                    base64_uri 1 image (27066 bytes)
                          fig_storage_path .matplotlib_figs/….png
                          hidden_to_model ['base64_uri']
```

The tool surface is unchanged — `run_python_code`, `run_code_in_interpreter`, `new_interpreter`, `delete_interpreter`, `list_interpreters`, `manage_interpreters` — as is the `base64_uri` / `hidden_to_model` contract the UI renders.

## Also here

A banner when a terminal opens, prepended to `initial_output` rather than printed by the shell: `/etc/bash.bashrc` runs for every interactive bash, including the `bash -i -c ...` the agent runs to execute a command, so a banner there would prepend itself to other people's command output. `PANTHEON_PTY_BANNER=0` turns it off.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ba23dc12f2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
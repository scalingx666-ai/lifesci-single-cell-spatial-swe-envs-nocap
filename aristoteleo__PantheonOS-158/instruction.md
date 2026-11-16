# Issue

**Title:** fix(file): list_files off the event loop, like read_file already is

## Description

## The symptom

A desktop opening on a freshly created sandbox, three calls in the same second:

```
file_manager.read_file      3.3 s
live_view.set_data_endpoint 3.3 s
pty.pty_write               4.3 s
```

The last one is the tell. `pty_write` does an `os.write` of a few bytes to a pty master. It cannot take four seconds, and it did not — it was waiting for a directory listing on the same event loop.

## Why

A workspace is a network-backed Modal Volume. `target_path.glob("*")` plus an `lstat()` per entry is a synchronous round trip **per entry**, and on a cold volume cache that is seconds rather than milliseconds. Run on the loop, it does not merely make the listing slow — it stops the agent, and every other request queues behind it regardless of who made it or what it was.

`read_file` was moved off-thread for exactly this reason (#154). `list_files` was not.

This is not a load problem: the same burst against a **warm** volume completes in **133 ms** end to end, every call ~110 ms.

## The change

Both paths — flat and recursive — run in `asyncio.to_thread`. The recursive one especially, since it walks far more of the volume.

## What it does and does not fix

The listing is no faster. That was never the problem. It stops taking everything else with it:

```
100 entries x 20 ms metadata each

on the loop (before)   listing 2319 ms | worst loop stall    0 ms | ticks    0
in a thread (after)    listing 2330 ms | worst loop stall   19 ms | ticks  211
```

`ticks 0` is a 10 ms heartbeat that never once ran while the listing was in progress — the loop was frozen for the full 2.3 s. Afterwards it ticks 211 times with a worst-case 19 ms stall, so a keystroke arriving mid-listing costs 19 ms instead of 2300 ms.

## Worth a follow-up, not in here

Other methods on this toolset do synchronous volume IO on the loop too — `create_directory`, `delete_path`, `move_file`, `write_file`. They are less hot than listing (which every file window does on open, and again on every reconnect) so this PR keeps to the one on the desktop's critical path. Happy to sweep the rest if you'd like it in one go.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
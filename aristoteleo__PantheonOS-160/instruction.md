# Issue

**Title:** fix(chatroom): the disk-usage walk was starving the event loop

## Description

## What was observed

A desktop was sluggish for roughly the first minute on a fresh sandbox — `get_cwd` 0.9 s, keystrokes 0.8–2.3 s — settling to ~60 ms afterwards. Sampled with py-spy against that sandbox, thirty seconds old:

```
Thread 33 (active): "disk-usage-walk"        96% CPU
    _walk_workspace_bytes (pantheon/chatroom/room.py:591)
    _refresh_disk_used     (pantheon/chatroom/room.py:699)

Thread 2 (idle): "MainThread"                 7.7%
    select (selectors.py:468)
```

One thread on a full core; the event loop idle behind it.

## Why the existing design did not hold

The walk was already moved to a daemon thread, deliberately, with the reasoning recorded in the docstring:

> os.scandir/stat release the GIL during the syscall, so the event loop keeps serving NATS RPCs while this runs.

True of the syscalls, not of the walk. The per-entry Python work — iteration, path building, the stack — runs with the GIL held. On a two-core sandbox the loop then has to contend for it, and `_ping`, which is answered by the RPC framework and touches no toolset, took **1674 ms** during that window against a **68 ms** median once things settled. A slow `_ping` is the cleanest possible signal here: nothing in it can be slow except the process itself.

## Two changes

**The walk yields.** A 1 ms sleep every 200 entries — sleeping, not `pass`, is what hands the GIL to a waiting thread. Measured with a 10 ms heartbeat alongside 40k entries of the same per-entry work:

```
as it was   walk  17 ms | ticks  0
yielding    walk 275 ms | ticks 25,  p50 11.0 ms,  worst 11.2 ms
```

`ticks 0` is a heartbeat that never once ran. The walk takes longer and stops being felt — the right trade for a number nobody is waiting on.

**It keeps out of the opening minutes.** The first `_ping` from a desktop arrives seconds after the agent starts answering, when the volume's FUSE cache is empty and every `stat` is a network round trip. So the first walk is simultaneously the most expensive it will ever be and the worst-timed — it lands while windows are opening and someone is typing into a terminal. Warm, the same tree (1614 files, 806 dirs, 5.7 GB) walks in **0.2 s**.

`_DISK_WALK_QUIET_SECONDS = 120`. Nothing waits on a disk-usage figure.

## Why not something cheaper than a walk

`statvfs` on the volume reports the mount, not the volume's contents:

```
/workspace -> total 409.6 GB, free 409.6 GB, used 0.0 GB
```

So the walk is the only way to get the number, and the question is only when and how politely it runs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
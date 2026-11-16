# Issue

**Title:** fix(chatroom): cache the misses, not just the hits

## Description

## What a keystroke was doing

py-spy, live sandbox, main thread, caught mid-keystroke:

```
exists (pathlib.py:860)
<genexpr> (chatroom/routed_memory.py:75)
_exists_in (chatroom/routed_memory.py:74)
_dir_for_chat (chatroom/routed_memory.py:84)
mgr_for_chat (chatroom/routed_memory.py:91)
_resolve_endpoint_for_chat (chatroom/room.py:394)
proxy_toolset (chatroom/room.py:1494)
```

Filesystem existence checks, on the event loop, per keystroke.

## Why

```python
def _dir_for_chat(self, chat_id):
    cached = self._chat_dir.get(chat_id)
    if cached and self._exists_in(chat_id, cached):
        return cached
    for cand in [self._active_dir, self._home_dir, *self._search_dirs]:
        if self._exists_in(chat_id, cand):
            self._chat_dir[chat_id] = cand      # ← hit is cached
            return cand
    return self._active_dir                     # ← miss is not
```

A hit is cached; a miss is not. So an id with no memory file re-runs the whole search **every time**: one `_exists_in` per candidate directory, three `stat()`s each, and on a network-backed workspace every one is a round trip.

Ids with no memory file are not the rare case. `ChatRoom.proxy_toolset` routes on `args["session_id"]`, and toolsets use that name for their own sessions — so a **pty session id arrives here on every keystroke** and never matches anything.

## Measured, from inside the affected sandbox

`pty_write` carries a `session_id`. `pty_list` does not. Same toolset, same path, same moment:

```
 t+s   _ping  pty_write  pty_list  get_cwd
   2      65       1519        63       64
   4      65         73        64       64
  26      63       1349        62       62
  28      62         72        63       63
```

Only the call carrying a `session_id` spikes. `_ping` — which does not go through `proxy_toolset` — never moves, so the event loop is not blocked by anything else.

Even with nothing pathological, the overhead is constant: `pty_write` 74 ms median against `pty_list` 62 ms, across 40 samples.

## The change

- **Misses are remembered for 30 s.** Short-lived on purpose: a new chat's file appears when it is first saved, and the answer for an unknown id — the active project — is what this returns anyway.
- **`_mgr` keys on the path as given** before falling back to `resolve()`, which is `realpath()` — another round trip, paid per call, for a directory that has not moved.

## Result

Against the real workspace, same directories, an unknown id:

```
as shipped   2.61 ms per lookup   (523 ms per 200 keystrokes)
patched      0.00 ms per lookup
```

That is with the volume warm. Cold, the same stats are what the 1519 ms was made of.

## Worth discussing separately

`proxy_toolset` reinterpreting an arbitrary toolset's `session_id` argument as a chat id. Caching makes it cheap, but it is still a collision between two unrelated meanings of one parameter name, and a pty session id now occupies an entry in a chat-routing cache. Happy to follow up if you want that tightened.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
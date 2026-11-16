# Issue

**Title:** feat(sandbox): keep the environment a user installs

## Description

## The report

> I installed vim, and the next time I went in it was gone. Surely a user's environment shouldn't be wiped by every update?

It is a fair complaint and the current answer is bad. Everything `apt` writes lands in `/usr` — the image — while only the Modal Volume survives. So a user's environment is erased by every sandbox recreation, and sandboxes are recreated **often**: on restart, after an idle reclaim, and on every agent-image update. An environment that cannot survive an update is not an environment.

This is much more visible now that the sandbox serves a real terminal (#156): people use it like a machine, and a machine that forgets is worse than no machine.

## Two halves

**1. The obvious tools ship in the image.**

A terminal with no editor and no pager is not a terminal. `vim` was command-not-found; so were `less`, `nano`, `htop`, `tree`, `jq`, `unzip`, `zip`, `file` and `procps`. About 35 MB on a 2.5 GB image, and it removes the most common reason to reach for apt at all.

**2. Anything else is declared, not accumulated.**

The persistent half of the filesystem cannot hold binaries in system paths — but it can hold the *instructions* for putting them back. The entrypoint now runs, on every boot:

```
~/.pantheon/on-start.sh
```

`HOME` is the Volume under the `default_workspace` layout, so that file persists. A user writes `apt-get install -y ripgrep` into it once and every future sandbox has ripgrep.

Declared rather than accumulated, which is the property that matters here: it **survives an image update instead of being wiped by one**, and it is inspectable and reproducible — unlike a container someone has been hand-editing for a month, which nobody can reconstruct.

## Forgiving on purpose

This runs before the agent, and the user wrote it:

- **Not fatal.** A bad line cannot cost someone their sandbox; the boot continues and the last 20 lines of output are logged.
- **Bounded.** `PANTHEON_SETUP_TIMEOUT` (default 300 s), so an accidental `read` cannot hang the boot forever.
- **Findable.** Output is copied to `~/.pantheon/on-start.log`, on the Volume, where both the user and support can read it after the fact.

Exercised locally across all four paths:

```
1) no hook            → boot proceeds, nothing logged
2) working hook       → [setup] ✓ finished
3) failing hook       → [setup] ✗ exited 9; continuing without it   (+ tail)
4) hanging hook (cap) → [setup] ✗ timed out; continuing without it
5) log on the volume  → on-start.log, on-start.sh
```

## Not in scope here

A UI for editing the hook, and a `packages.txt`-style declarative form on top of it. The shell script is the primitive; both of those are sugar over it and belong in the frontend.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
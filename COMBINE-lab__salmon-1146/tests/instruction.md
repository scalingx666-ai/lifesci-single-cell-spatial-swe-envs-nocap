# Issue

**Title:** Disk-aware deterministic intermediate: `--radScratchDir`, space preflight, fast ENOSPC, failure cleanup

## Description

Second maintainer-side item from #1140 — the "disk: yes, it needs more than documentation" section of @BenjaminDEMAILLE's review, ahead of the default flip.

- **`--radScratchDir <dir>`** — place the salmon-owned intermediate on node-local scratch or memory-backed storage (`/dev/shm`), pid-suffixed so concurrent runs can share a scratch volume. On Linux this is also our answer to the in-memory RAD store: OS-managed memory placement with graceful spill and no new I/O machinery. Explicit `--writeRad` wins, with a warning if both are given.
- **Startup preflight** — warn when the target volume has less free space than the total compressed input. Deliberately a warning against a proxy rather than an error against a constant: Ben measured 14.6 vs 57.6 bytes/fragment between fixtures of the same read count, so per-fragment estimates aren't safe to hard-fail on.
- **Fast ENOSPC** — the RAD writer probes free space every 256 MiB appended and errors (naming the path, the free space, and the two mitigations) once free space drops under 512 MiB, instead of failing at the end of the mapping pass.
- **Failure cleanup** — when salmon owns the intermediate path: failed phase 1 removes the `.partial-*` leftover, failed phase 2 removes the finalized intermediate (previously leaked). User-named `--writeRad` paths are never cleaned.

All three two-phase drivers (reads `--deterministic`, `-a --deterministic`, genome projection) get identical treatment. `free_disk_bytes` (statvfs) is the workspace's only `unsafe`, documented and confined to `salmon-core` (reports `None` off-Unix, and callers treat `None` as "cannot check", never "no space").

Verified end-to-end: intermediate lands pid-suffixed in the scratch dir, `quant.sf` byte-identical with and without it. Unit tests cover placement, pid-suffixing, and cleanup semantics. Workspace suite 293/0; clippy/fmt clean. Docs updated (CLI reference + the RAD/determinism guide gains a "disk use" section with the measured sizing guidance).

Stacked on #1143 (shares the `run_deterministic` edits); the diff below includes it until that merges.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c498cbf07244`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
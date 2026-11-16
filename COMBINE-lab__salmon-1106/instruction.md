# Issue

**Title:** fix(rad): never leave a truncated RAD under the requested name

## Description

Writer-side half of #1105. The reader-side hang is being fixed upstream in libradicl (COMBINE-lab/libradicl#45); this closes the hole that produced the bad file in the first place.

## What went wrong

A run whose RAD write failed on a full disk **exited 0** and left a truncated file at the path the user asked for. A later `--rad` run then read that file as though it were complete and hung. Three separate defects lined up:

**1. The write result was discarded.** `flush_rad` is the only point at which RAD bytes reach the filesystem, and it ended in:

```rust
let _ = rad.append_chunk_bytes(&bytes);
```

Both per-record buffer writes were `let _ = ` too. `ENOSPC` was therefore structurally invisible. These now propagate and the run fails loudly.

**2. Bytes went straight to the destination.** Output is now written to a sibling `<name>.partial-<pid>` and renamed into place only after a successful finalize. Rename rather than delete-on-error because it is atomic and also covers `SIGKILL`, where no cleanup code of ours would run at all. Keeping the temp file next to the destination (not in a temp dir) keeps the rename within one filesystem; a cross-device rename would degrade to a copy and reopen the very window this closes.

Write errors name the partial explicitly:

```
Error: quantification failed

Caused by:
    mapping failed: FASTX error: Error reading from buffer: writing RAD chunk to /path/out.rad.partial-2629896
      the incomplete file has been left there; it is NOT usable as `--rad` input: couldn't write chunk bytes to RAD file: File too large (os error 27)
```

`finalize` also now flushes via `into_inner` + `sync_all` instead of dropping the handle. Dropping a `BufWriter` flushes but swallows the error, and on NFS a deferred `ENOSPC` surfaces only at that point — which is exactly where the original report came from.

**3. Nothing recorded completeness.** `finalize` sets a `WRITE_COMPLETE` bit in `baked_flags`.

To be explicit about the contract, since this came up in discussion: **this bit is confirmatory only.** Its presence proves the file was fully written; its absence proves nothing, because a conforming producer may stream a RAD file without ever backpatching — the same reason `num_chunks == 0` is a valid "unknown chunk count" signal rather than a corruption signal. Readers may use it as a fast path but must never require it, or they would reject legitimate files from other tools. No reader-side rejection is added here.

## Verification

Simulating a write failure **without filling a device**: `ulimit -f` caps the file size a process may create, so writes past the cap fail with `EFBIG` — the same class of failure as `ENOSPC`.

```bash
ulimit -f 4        # 2 KiB
trap '' XFSZ       # take the error return rather than the signal
salmon quant -i idx -l A -1 r1.fq -2 r2.fq -o out --writeRad out.rad -p 2
```

| | before | after |
|---|---|---|
| exit code | 0 | 1 |
| error reported | none | names the partial file |
| file at requested path | truncated `out.rad` | absent |
| leftover | — | `out.rad.partial-<pid>` |

Happy path re-checked end to end: `--writeRad` produces the file at the requested name with no partial left behind, and a `--rad` run consumes it and produces the expected `quant.sf`.

Two regression tests in `salmon-rad`. Negative control run on the first: reverting the temp path to `File::create(path)` makes `abandoned_write_never_claims_the_final_path` fail, so it catches the actual bug rather than passing vacuously.

`cargo fmt`, `clippy --workspace --all-targets -D warnings`, and the full workspace suite are clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e61a213d3fa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
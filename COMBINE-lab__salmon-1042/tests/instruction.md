# Issue

**Title:** perf(align): reuse query buffer and LUT-encode DNA5 (~14% faster full-length, byte-identical)

## Description

## Summary

Two **profiling-guided, behavior-preserving** optimizations to `align_chain`,
salmon's per-candidate selective-alignment validation (called millions of times).
Output is **byte-identical** (all map/quant tests pass, including the end-to-end
determinism test). Independent of any other change.

## What & why

Profiling a single-threaded reads run (1M pairs, Apple M4 Max, macOS `sample`)
showed `--fullLengthAlignment` is dominated by alignment (~65%), with the
per-candidate query allocation and DNA5 encoding a measurable share:

- `align_chain` built its oriented query with a fresh `read.to_vec()` /
  `revcomp()` **per candidate** → now reuses a thread-local buffer via a new
  `revcomp_into` helper (one fewer heap allocation per candidate).
- `dna5_encode` did a per-base `match` (a compare chain) → now uses a 256-entry
  lookup table, since encoding the read + reference window is on the inner loop
  of every full-length score.

## Result (measured, `-p 1`, 1M read pairs, M4 Max)

| Mode | before | after | |
|---|---|---|---|
| `--fullLengthAlignment` | ~6.55s | **~5.64s** | **~14% faster** |
| anchored (default) | ~1.72s | ~1.70s | unchanged (within noise) |

The default anchored path is unchanged on purpose: profiling shows its cost is
dominated by **chaining (~30%) and index hit-search (~28%)** — the latter in
external crates (`piscem-rs` / `sshash-lib`) — so there is little allocation
headroom there (alignment is only ~10% of the default path). This PR targets the
part that pays off.

## Tests

`cargo test -p salmon-map` and `cargo test -p salmon-quant` green; `quant.sf`
byte-identical before/after.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb7aa8aa84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
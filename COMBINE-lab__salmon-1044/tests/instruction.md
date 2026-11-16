# Issue

**Title:** Mapping perf (radix sort ~2%) + richer meta_info.json & bad-input diagnostics

## Description

Two independent, self-contained improvements to the reads/alignment quant paths — no upstream (piscem-rs / sshash-rs / libradicl) bumps required, so this is a salmon-only change.

## 1. Mapping perf: radix sort for the `(tid, fw)` grouping (~2%)

`candidates_from_raw_hits_true_unimems` (`crates/salmon-map/src/extend.rs`) groups the full per-read raw-hit set by `(tid, fw)` before diagonal chaining. Profiling at `-p16` (compute-bound, IPC ~2.1) pinned this integer-keyed grouping sort as the single largest self-time bucket (~14%, dominated by high-N repetitive reads).

Replace it with a length-dispatched **LSD radix sort** on key `(tid << 1) | fw` (radix for N ≥ 256 hits, `sort_unstable` below), reusing per-thread ping-pong scratch. The grouping sort's output order within a group is discarded (each group is re-sorted by diagonal in `merge_same_diagonal`), so the result is **byte-identical**.

- **Byte-identical** `quant.sf` in both SA and sketch modes (verified).
- **~2% faster mapping** at every thread count (same-input scaling, `--skipQuant`): p1 −2.6%, p8 −1.6%, p16 −1.8%.

## 2. QoL: richer `meta_info.json` + zero-cost bad-input diagnostics

All derived from **end-of-run aggregates** (evaluated once, never per-fragment) and emitted for **every mode** — reads, `-a` alignment, and `--rad`. Shared `Diagnostic` / `input_diagnostics()` / `peak_rss_kb()` live in `salmon-core`.

**New `meta_info.json` fields** (salmon-rs extensions beyond the C++ schema; C++-only consumers ignore them):
`pos_bias_correct`, `num_orphan` (reads), `range_factorization_bins`, `num_em_iterations`, `em_converged`, `detected_library_type`, `total_time_seconds`, `peak_rss_kb`, and a structured `diagnostics[]` array.

**`diagnostics[]`** — machine-readable `{code, severity, message}` red flags (also logged), so pipelines can gate on codes instead of scraping logs:

| code | severity | fires when |
| --- | --- | --- |
| `no_input_fragments` | error | zero fragments processed |
| `no_fragments_mapped` | error | zero fragments mapped (wrong reference) |
| `very_low_mapping_rate` / `low_mapping_rate` | warning | < 10% / < 30% mapped |
| `library_type_mismatch` | warning | explicit `-l` disagrees with observed format (reads / `--rad`) |

The library-type check runs the detector even under an explicit `-l` (it samples orientation pre-strand-filter), and **never overrides the user's `-l`** — verified `-l ISR` on IU-observed data warns while `library_types` stays `[ISR]`.

Docs: `reference/output-formats.md` gains a salmon-rs-extensions table + the diagnostics code/severity table.

## Testing
- `cargo build` + full `salmon-map` / `salmon-core` / `salmon-quant` / `salmon-align` test suites pass (14 suites).
- clippy clean, `cargo fmt` applied.
- End-to-end: verified new JSON fields + firing diagnostics on reads (`no_fragments_mapped` from random reads; `library_type_mismatch` from `-l ISR`) and on `--rad` (baked-format mismatch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01B7JMur5DmDpECddErpi2JS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54cdd903162f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** fix(infer): read multi-sample row names; finish when --quant-subset names absent barcodes

## Description

## Summary

Fixes two `infer` bugs found while reviewing #204. Both are on `develop` and in 0.18.3 and were not introduced by #204.

1. **`infer` panics on multi-sample input** (10x Flex). A multi-sample `quant` names its rows `<sample>_<barcode>`. `infer` read each row name as a bare barcode k-mer, with the k-mer length taken from the first row, and aborted with `can't extract kmer`. So `quant -d` → `infer` has never worked on Flex.
2. **`infer --quant-subset` hangs** when the list names a barcode the matrix doesn't have. The workers stop after as many cells as the list has entries, so a missing barcode leaves them waiting forever. In a multi-sample run, a barcode shared by several rows also gives a wrong count.

## Changes (`src/infer.rs`)

- Row names are read as text and written to the output unchanged. `infer` now errors if `quants_mat_rows.txt` doesn't have one name per matrix row; previously the zip silently truncated.
- The rows to keep are worked out first, and the worker stop count is the number of rows kept.
- **`--quant-subset` lines:**
  - A line naming a row (`<sample>_<barcode>`) keeps that row.
  - A bare barcode keeps that barcode in every sample.
  - Bare barcodes are still compared as k-mers of the row barcodes' length, as before, so single-sample lists behave the same, including a Cell Ranger `-1` suffix being ignored.
  - Blank lines are skipped instead of causing a panic.
- `infer` no longer uses `permit_list_from_file` or `read_filter_list`; both are still used by `cellfilter` and `quant`, which are unchanged.

## Testing

- **New tests:** `tests/infer_rows.rs` (4 tests) runs the binary on a hand-built multi-sample input. It checks:
  - row names and per-row counts;
  - a bare barcode kept in two samples, plus an absent barcode;
  - a named row kept alone;
  - a single-sample list with a `-1` suffix and an absent barcode.

  On `develop`, the multi-sample tests fail with the panic, and the single-sample one is killed after 60 s.
- **Full suite:** 135 tests pass; clippy and fmt are clean.
- **PBMC1k** (`quant -d -r cr-like` → `infer`):
  - the output matrix matches `develop`'s exactly (1,024,620 entries, 0 differing);
  - a `--quant-subset` of 3 present barcodes plus 1 absent one finishes and gives the same matrix as `develop` on the 3 present ones (`develop` hangs).
- **10x Flex v2, 384-plex** (`quant -d` → `infer`):
  - finishes: 261,865 rows × 18,132 genes;
  - each row's total equals its equivalence-class count total (196,660 nonempty rows, 0 differing);
  - a subset of 3 named rows plus a bare barcode found in 3 samples keeps 6 rows, with values identical to the full run.

## Merge notes

- `develop` (with #204, b3c7d70) is merged into this branch. The conflicts with #204 kept both sides: the `infer.rs` imports, the `-c` note in `infer.rst`, and the CHANGELOG `### Fixed` section. The merged tree is identical to the tested trial merge; 150 tests pass.
- With both changes in place, `quant-probe -d` → `infer` is still refused, and Flex `infer` output is unchanged.
- Intended for 0.19.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01TtmwfkBMvwsCxdQrf4RTPN

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3c7d707258e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
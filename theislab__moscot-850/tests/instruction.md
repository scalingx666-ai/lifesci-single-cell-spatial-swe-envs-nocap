# Issue

**Title:** perf(sparsify): partition out the max_k largest entries in mode='mass'

## Description

## Summary
With `max_k` set, `sparsify(mode="mass")` keeps at most `max_k` entries per row, yet `_mass_select_block` sorted every full row and built the result from a dense mask. It now partitions out the `max_k` largest entries (`np.argpartition`), sorts only those, and builds the CSR from the kept entries. The output is unchanged; row totals are summed in row order rather than sorted order, which can differ in the last bit.

## Timing
One block of 2,048 rows x 180,896 columns of a real coupling, single thread:

| | before | after |
| --- | --- | --- |
| `value=0.95, max_k=100` | 22.8 s | 1.9 s |
| `value=1.0, max_k=50` | 26.3 s | 3.0 s |
| `value=0.5, max_k=None` | 23.6 s | 20.4 s |

Sparsifying the three couplings of a 487k-cell `TemporalProblem` with `max_k=100` (via CellRank's `RealTimeKernel.from_moscot`) took 92 min before (on a GPU node, the sort on one CPU core) and 13 min with this selection (on a CPU node).

## Testing
- `tests/solvers/test_base_solver.py` and the sparsify tests of `tests/backends/ott/test_backend.py`: 185 passed.
- New `test_sparsify_mass_matches_reference` checks against a per-row reference for `value` in {0.3, 0.9, 1.0} and `max_k` in {1, 5, 40, m, None}.
- On real coupling rows (3 blocks x the 3 settings above) the result equals the current release's.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01CEkHnYavwEf7n32j7rNkPv

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `440093ccbb8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
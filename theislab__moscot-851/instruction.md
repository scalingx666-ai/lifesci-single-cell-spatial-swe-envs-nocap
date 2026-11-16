# Issue

**Title:** perf(sparsify): select mode='mass' entries on the device for ott outputs

## Description

`sparsify(mode="mass", max_k=...)` copied every `[batch_size, m]` block of rows to the host to keep at most `max_k` entries per row. For ott outputs the rows are built on the device, so this selects there and copies only `[batch_size, max_k]` per block.

- `BaseDiscreteSolverOutput._mass_select` is a new hook for the `mass` rule; its default is the existing numpy selection. `OTTOutput` overrides it when the rows are a `jax.Array` and `max_k` is set, using `jax.lax.top_k` over 256 rows at a time: one `top_k` over a 2048 × 92,507 block needed several times the block's memory and ran 3x slower.
- It keeps the same entries as the host selection, except among tied entries (e.g. rows of low-rank outputs), where an equal value may be kept at another column. The new test compares the kept values per row.

Two Sinkhorn couplings from a single-cell time course, `value=0.95, max_k=100, batch_size=2048`, RTX 4090:

| coupling | host selection (as in #850) | device selection |
| --- | --- | --- |
| 47,842 × 55,104 | 193 s | 0.98 s |
| 55,104 × 92,507 | 384 s | 1.86 s |

Same number of entries in both; 22 and 60 rows keep a tied entry at another column (values differ by < 1e-7). On CPU, one 2048 × 92,507 block takes 0.99 s with numpy and 0.68 s with jax.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01CEkHnYavwEf7n32j7rNkPv

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b90f31e17ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
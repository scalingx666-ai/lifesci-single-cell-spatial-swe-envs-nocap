# Issue

**Title:** fix(em): shard partition must come from the data, not the thread count (release blocker)

## Description

Two defects in the same six lines of the parallel M-step. One of them **blocks the 2.6.0 tag**.

## Release blocker: output is not reproducible across thread counts

`nshards = rayon::current_num_threads().clamp(1, 64)` made the shard count — and therefore the class partition, and therefore the grouping of the floating-point sums — a function of `-p`.

On 26.1M real fragments over 238k transcripts, **`-p 4` and `-p 32` produce different `quant.sf` at default precision.** The mechanism is confirmed by construction:

| run | shards | md5 |
|---|---|---|
| `-p 64` | 64 | `2806257f4199b632` |
| `-p 80` | 64 (clamped) | `2806257f4199b632` — identical |
| `-p 16` | 16 | `09388738c3935bff` — differs |

Same shard count ⇒ same answer. Different shard count ⇒ different answer. The thread count itself is irrelevant; the shard count is the whole variable.

This is the guarantee the deterministic default exists to provide. **The existing suite could never have caught it** — its fixtures hold a handful of eq classes, where every partition is the same partition. That's a fixture problem as much as a code problem, so the new test is built to shard several times over.

The partition now derives from the class count alone. Rayon still spreads those shards across whatever threads exist — scheduling can't change arithmetic. The new plan reproduces exactly what the old code computed at `-p >= 64`, so **large-thread results are unchanged** and smaller runs now agree with them.

## Scaling: the dense clear/reduce @rob suspected

Every shard cleared a full `num_txps` buffer, and `reduce_shards` summed every shard for every transcript — `O(nshards × num_txps)` per iteration regardless of the data. About **30M operations per iteration** at 64 shards against ~1.3M eq-class entries of real work. The overhead grew with thread count while the work stayed fixed, which is why the EM stopped scaling past ~32 threads and then regressed, capping the deterministic path at 1.5× from 8→64 threads on a Broadwell box where online reached 1.9×.

The touched-transcript optimization was indeed missing. Class labels never change between iterations, so each shard's reachable set is computed once and the clear touches only those.

The reduction needed more thought: a sequential scatter-add is deterministic but serializes ~3.6 billion adds over a real run. So the touched sets are inverted into a CSR index (transcript → contributing shards, ascending), making each output element an independent fixed-order sum — parallel and deterministic at once.

## Measured (26.1M fragments, gencode v49, sketch, same binary pair)

| `-p` | before | after | speedup |
|---|---|---|---|
| 4 | 70.10 s | 68.26 s | 1.03× |
| 16 | 25.06 s | 23.59 s | 1.06× |
| 32 | 21.41 s | 18.80 s | 1.14× |
| 64 | 20.01 s | 17.06 s | **1.17×** |

The gain grows with thread count, as the diagnosis predicts. On the spinning-disk Broadwell box at `-p 16` it moves deterministic from 9.1% behind online to **3.6%**; higher thread counts still measuring.

## Tests

The regression test compares bit-for-bit across rayon pools of 1/2/3/8/16 threads, with weights chosen so the sums are not exactly representable (tidy powers of two would agree under any grouping and prove nothing). **Verified to fail on the pre-fix tree** — 1809 of 5000 transcripts differ between 1 and 2 threads. A test that passed on the broken code would have been worthless. A second test pins the shard count as independent of the pool.

Suite **340/0**, clippy clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `909b21b11a16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
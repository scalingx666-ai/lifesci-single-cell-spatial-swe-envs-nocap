# Issue

**Title:** deps: paraseq-temp 0.5.0-pre.2 (parked worker pool, upstream 0.5.0)

## Description

Moves to the pre.2 republication: upstream paraseq's **released 0.5.0** plus the redesigned resizable pool ( — fixed spawn set with parking, worker count bounded by construction). Lockfile-only for the dependency; piscem-rs 0.9.1's requirement admits pre.2.

`pool_resize_flush_safety` is reworked for parked semantics: the old non-vacuity guard counted worker incarnations exceeding the ceiling, which parking makes impossible **by design** — it failed for exactly the right reason. The new guard requires each shrink to be *observed* taking effect (pool at/under target), ≥5 times per run.

**Evaluated end to end** at `-p 64 --decoder parallel` on 26.1M real read pairs: SA 58s / sketch 35s / SA+det 58s / sketch+det 32s, all mapped counts identical to every prior run — and `quant.sf` **byte-identical** (238,443 rows) between serial and parallel decoders under `--deterministic`. 278 workspace tests, clippy clean.

No version bump; release deferred until this has soaked. Companion PR: COMBINE-lab/piscem-rs#5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a97c176bf13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
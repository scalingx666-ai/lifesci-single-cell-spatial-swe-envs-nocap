# Issue

**Title:** Adopt the adaptive thread broker (piscem-rs 0.9.0, paraseq-temp)

## Description

## What this is

Adopts piscem-rs's adaptive thread broker in salmon: `-p` becomes a single
execution-slot budget shared between gzip decoding and mapping, solved from
live measurement rather than split by a fixed guess. Includes `--decoder`
(auto/serial/parallel/parallel=N) and `--threadPolicy <FILE>`.

**Ready for review.** Every stage below is verified; nothing is provisional.

## Dependency changes

- **piscem-rs 0.6.4 → 0.9.1** (`rapidgzip` feature on). 0.7.x/0.8.0 were yanked
  upstream; 0.9.1 additionally requires the pool fix below.
- **paraseq 0.4 → paraseq-temp 0.5.0-pre.1** — required, not incidental:
  `ThreadPool` is the resize mechanism the broker acts through. Lib target is
  still `paraseq`; no import changes. `paraseq` remains the official crate;
  move back at 0.5.0.
- **thread-broker 0.1.0**, **rapidgzip-core ≥ 0.3.1** (transitively pinned).

## A deadlock found, rooted, and fixed upstream

Enabling the broker on paired input at `-p ≥ 48` hung salmon. Bisect: the split
was not the variable (pinned `parallel=4` plans the identical 56/8 split and
completes — pinning disables the broker, which is the trigger); paired input
and thread count were. Backtraces showed a permit-starvation picture in
rapidgzip's shared `DecoderPool`.

Root cause — **not in salmon, not in paraseq**: a lost wakeup in
`DecoderPool::release`, which notified waiters without holding the scheduler
lock. The final release could land between a waiter's admission check and its
park, leaving free permits, parked decoders, and no future notify. piscem never
reproduced it because its decode share keeps admission off the contended path;
salmon's heavier consumer drives the broker to shrink the pool, which is what
makes the window reachable. Fixed in **rapidgzip-core 0.3.1** with a regression
test that deadlocks the unfixed pool in <2 s; **piscem-rs 0.9.1** requires it.
Verified here: all six previously-hanging configurations complete (37–62 s)
with mapped counts identical to their serial-decoder runs. Full narrative:
`notes/pool-lost-wakeup-deadlock.md`.

## Engagement thresholds: measured, all four cells

`min_threads_per_stream = 1 + C/P`, read from the broker's own solved
`producer_cost_share` at `-p 64` on 26.1 M paired human RNA-seq fragments:

| cell | share | threshold |
|---|---|---|
| sketch | 0.094–0.100 (×3) | **10** |
| sketch + `--deterministic` | 0.110 (×2) | **9** |
| selective alignment | ~0.02 | **50** |
| SA + `--deterministic` | ~0.01 (not resolvable from SA) | **50** |

- Sketch confirms the `--deterministic` prediction: lighter mapping → higher
  producer share → earlier engagement. Thresholds round down because the
  measured cost asymmetry favours engaging (missing parallel cost up to 4.2×;
  engaging needlessly cost 8–28%).
- SA's figure carries an honest error bar (a CPU-ratio cross-check suggests
  ~24) but its content survives it: with paired input, even the low estimate
  engages only at `-p ≥ 48`. Serial decode is simply right for SA at nearly
  every real budget — which the theory predicted and the wall clocks confirm
  (SA parallel ≈ SA serial at `-p 64`).
- SA's `--deterministic` delta is not resolvable: alignment scoring dominates
  its cost, and the deterministic pass strips bookkeeping that is a large
  fraction of sketch's cost and a small one of SA's. Constants set equal; the
  test asserts `≤`, not an invented `<`.

## Safety under a resizable pool

- `quant.sf` **byte-identical** to pre-change `develop` at `-p 1` (238,443
  rows), serial decoder both sides.
- Thread-local flush contract pinned by test: counters merged at thread end,
  output buffers flushed per batch and at retirement, `Clone` rebuilds fresh
  state. The test churns the pool through ~134 real retire/respawn cycles and
  asserts exactly-once delivery **by id**, with a non-vacuity guard.
- The decoder decision is **per input file** (metadata-only classification —
  a FIFO is never read), pinned by tests: a plain file among gzip inputs does
  not cost them the parallel decoder, and no slots are reserved for decoders
  that don't exist.

## Verification

277 workspace tests, clippy clean, zero non-registry dependencies in the
lockfile.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `987341dddfce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** fix(rad): drain the queue before workers exit (silent zero/partial counts)

## Description

`salmon quant --rad` and alignment mode could **silently return zero or partial counts** — an empty `quant.sf`, no error, no warning.

Found while chasing the intermittent aarch64 failure of `rad_input::thread_count_invariant`.

## The race

libradicl's producer pushes **every** meta-chunk into the queue and only then sets `done`. Salmon's workers exited on:

```rust
if let Some(mc) = queue.pop() { … }
else if done.load(Ordering::Acquire) { break }   // ← exits with a full queue
```

A worker whose `pop()` comes up empty in the window *just before* the producer pushes will then observe `done == true` and break, abandoning every chunk. Four worker loops in `rad.rs` had this shape; each now takes one more sweep after first observing `done`.

## Demonstrated, not inferred

Forcing the window open (150 ms sleep between the empty `pop()` and the `done` check), on x86_64, deterministically:

| | `num_processed` | `num_mapped` | `eq_classes` | counts |
|---|---|---|---|---|
| **unfixed** | 0 | 0 | 0 | `[0.0, 0.0, 0.0]` |
| **fixed** | 487 | 487 | 4 | `[167.31, 211.0, 108.69]` |

## It is not a thread-count bug

Despite where the flaky test pointed. The instrumented CI reproduction:

```
[t=1 ] processed=487 mapped=487 eq_classes=4 em_iters=50    counts=[167.31, 211.0, 108.69]
[t=8 ] processed=487 mapped=487 eq_classes=4 em_iters=50    counts=[167.31, 211.0, 108.69]
[t=1b] processed=0   mapped=0   eq_classes=0 em_iters=10000 counts=[0.0, 0.0, 0.0]
```

`t=1` and `t=8` **agree perfectly**; the failure is `t=1b`, the *repeat* of the 1-thread run. Any worker can lose the race — a lone worker just has nobody to cover for it.

This is also distinct from #1056, which addresses f64 non-associativity in the M-step reduction. That produces last-bit differences; it cannot turn 487 into 0.

## The existing test could not catch this

`thread_count_invariant` asserts only that three runs **agree**. With the window forced open, all three returned zero and **the test passed**. The CI flakiness that surfaced this was the *lucky* partial case.

So the new test asserts absolute correctness — `num_processed == 487`, mass conserved, at `-p` 1/1/2/8 — and I verified it fails on unfixed code with the race forced:

```
assertion `left == right` failed: -p 1: reader dropped fragments (0 of 487)
```

A regression test that cannot fail proves nothing.

## Upstream is not at fault

| | verdict |
|---|---|
| libradicl library | ✅ never pops from the queue itself — no instance of this |
| libradicl examples (×2) | ❌ both use the racy shape |
| alevin-fry (×4 sites) | ✅ all guard with `\|\| !q.is_empty()` |
| salmon (×4 sites) | ❌ this PR |

Reporting the examples upstream separately, with a proposal for a drain-safe iterator so consumers stop hand-rolling the contract.

## Rarity

~1 in 600 whole-binary runs under CI stress on aarch64; never observed on x86_64 outside forced conditions; most likely at low thread counts. Worth noting in the 2.4.1 release notes given the failure is silent.

## Validation

`cargo test --workspace --release`: 27 binaries, 0 failures. `cargo fmt --check` clean. Clippy at the 9 pre-existing warnings.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01R5jNNvJnFRiu2eC1JZAu2T

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60faaa680ff8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
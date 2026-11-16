# Issue

**Title:** fix(quant): gate the auxiliary models on assigned fragments

## Description

.

The eq-class path opened the auxiliary-model burn-in gate on `num_processed`:

```rust
let use_aux = sh.num_processed.load(Ordering::Relaxed) >= sh.pre_burnin;
```

`num_processed` counts every fragment reaching `record` — including ones with no mappings at all, and ones whose mappings were all library-incompatible. But the auxiliary models are only *trained* on assigned fragments. So the gate opened before the models had seen `pre_burnin` observations, by a margin that widens as the mapping rate falls: at 92% mapped the gate opens ~8% early, and on a poor library considerably more.

The fix gates on assigned fragments, which is what the two things it should already have agreed with do:

- the online path immediately above, which reads `online.num_assigned()`
- C++ salmon's `useAuxParams`, which tests `localNumAssignedFragments + numAssignedFragments` against `numPreBurninFrags`

`fetch_add` returns the pre-increment count, and that is the value wanted here — the online gate reads its counter before its own increment, and C++ evaluates `useAuxParams` before counting the current read. Using the post-increment value would gate a fragment on a total that includes itself, differing from both by one.

### On the per-thread alternative

A per-thread counter was raised as an option. Rejecting it: the behavior being gated is *shared*, so gating it on a per-thread quantity would make the switch-over point depend on the thread count, which is not something a user's results should turn on.

`clippy -D warnings` and the `salmon-quant` suite are clean. Effect on real data to follow in a comment.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e61a213d3fa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
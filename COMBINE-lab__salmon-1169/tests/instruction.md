# Issue

**Title:** docs: measured 2.6.0 figures, EM architecture briefing, and strong types for the init/eff-lens footgun

## Description

Stacked on #1167 (retarget to `develop` when that merges). Three commits.

## 1. Replace the 2.6.0 performance and disk figures with measured ones

The slow-disk validation on `newton` (#1140) measured several things the release notes asserted from a single machine.

- **Speed is now hardware-qualified.** "As fast or faster in every measured cell" is not true generally: on a Xeon E5-2699 v4 with 26M real fragments, deterministic is ~4% slower at `-p 16` and ~12% slower at `-p 32`, then **twice as fast at `-p 64`**. The notes also now carry the predictability difference, which matters more than the mean for pipeline sizing — across four repeats at `-p 64` the online path ranged **55–105 s (bimodal)** while deterministic held 39–42 s.
- **Reproducibility restated honestly.** It claimed "md5-identical at `-p 1/4/16`" on the strength of a 400-read fixture that could not have exposed a difference. Now: byte-identical at every thread count on 26M fragments at full `--sigDigits 9` precision, naming the test that enforces it.
- **The disk section leads with the finding**: disk speed is not a factor. Writing the RAD is hidden behind mapping compute (30.55 s on spinning disk vs 30.92 s in `/dev/shm`); reading it back is decompression-bound, not I/O-bound.
- **Two figures were simply wrong**, both understating the product: RAD size quoted as ~110 MB per 1M read pairs, measured **45 MB (sketch) / 55 MB (SA)**; `--radCompress zstd` quoted as ~30% shrink at ~11% wall, measured **53% at ~5.5%**.

## 2. `docs/em-architecture-and-optimization.md`

A briefing for whoever evaluates further EM optimization, so effort goes somewhere new rather than re-deriving what is here. Covers the CSR layout and its real scale, all four M-step kernels, the `ShardPlan` from #1167 with **the four determinism invariants any future change must preserve**, the convergence check, and the three acceleration loops.

It deliberately records **what has already been tried and rejected, with reasons** — shared atomic accumulator (CAS contention), caching the inner product in scratch (memory traffic beat the multiply), thread-derived shard counts (that is the #1167 bug) — and ranks the remaining candidates. Top of the list: each shard's dense 238k-entry accumulator gives a **122 MB working set against ~55 MB of L3**, and since `touched[s]` is now computed anyway, index-compressing each accumulator to its own touched set should cut that to ~10 MB without disturbing determinism.

Full test-data provenance on `newton` is included: paths, both binaries staged for A/B, the dataset and the scale it produces, how to extract per-phase timings (including the ANSI-escape trap that broke my first parser), a **verified** table of which flag selects which kernel, and the benchmarking caveats learned the hard way — warm the page cache, do not interleave arms, and treat any single-run `--online` comparison at high `-p` as meaningless.

## 3. Strong types for the `init_alphas` / `eff_lens` swap

`run_em_counts` takes `init_alphas: Option<&[f64]>` immediately followed by `eff_lens: Option<&[f64]>`. Structurally identical, so swapping them compiled silently — and it **shipped that way**: the bootstrap path passed effective lengths into the `init_alphas` slot, leaving `--perNucleotidePrior` inert inside every replicate *and* warm-starting each replicate from the effective-length vector. Reported spread was drawn under a different prior than the estimate it quantified.

A comment is not a guard. They are now distinct newtypes, converted across all four crates and 16 call sites:

```rust
run_em_counts(p, counts, opts, parallel, min_iter,
              InitAlphas::NONE,             // or InitAlphas::new(&warm)
              EffLens::new(&eff_lengths))   // or EffLens::NONE
```

Three properties keep it from decaying:

- **Zero overhead is asserted, not claimed** — `const _: () = assert!(size_of::<EffLens>() == size_of::<Option<&[f64]>>())`. Both 16 bytes; a fatter wrapper stops the crate compiling.
- **The swap is proven impossible** by a `compile_fail` doctest on `InitAlphas` that runs in CI and doubles as API documentation.
- **No `Deref`, no `Into<Option<..>>`**, deliberately — implicit conversion back to the bare type would reopen the hole. Accessor is `pub(crate)`.

The compiler found every affected site once the types diverged, including one a manual sweep would likely have missed (`init_alphas.as_deref()` in the online alignment path, which needed a `map_or` rather than a substitution).

Suite **343/0**, clippy clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0300044ea2aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** chore(deps): migrate to rand 0.10 / rand_pcg 0.10 / rand_distr 0.6

## Description

Reopens #1069, which GitHub auto-closed when its base branch (`chore/pre-2.4.0-dep-updates`) was deleted on merging #1068. Same branch, same commit (`6e7d2df1`), now targeting `develop` directly.

The last deferred dependency group.

```
rand        0.8 -> 0.10
rand_pcg    0.3 -> 0.10
rand_distr  0.4 -> 0.6
```

**No code changes.** The three move together because `rand_distr` 0.6 needs `rand_core` 0.10; bumping `rand_pcg`/`rand_distr` alone leaves `Rng` coming from rand_core 0.6 and fails to compile, which is what made this look invasive when it was first deferred. With all three aligned, `Pcg64Mcg::seed_from_u64` and `Distribution::sample` work exactly as written.

Collapses `rand` from three versions in the tree (0.8.7, 0.9.5, 0.10.2) to one.

## Output is unchanged, including the RNG-backed paths

| output | result |
|---|---|
| `quant.sf` (point estimate) | **byte-identical** |
| `bootstraps.gz` | **byte-identical** |
| Gibbs samples | **identical to ~1 ULP** |

Seeding survives because `rand_core`'s `seed_from_u64` is byte-identical between 0.6 and 0.10 — same PCG32 expansion, same `MUL`/`INC` constants, same output function — so a given seed still produces the same PCG stream.

## The Gibbs result needs care, because a byte comparison misreads it

The Gibbs files *do* differ, which initially looked like `rand_distr`'s `Gamma` sampler drawing a different stream — and it was reported that way before being measured. Measuring the magnitude shows otherwise, over 256 samples × 15 transcripts:

```
max |Δ|          = 1.8e-12
max relative Δ   = 7.4e-16          (~1 ULP for f64)
differing values = 1730 / 3840      (last bit or two)
```

A different random stream would give O(1) differences, not O(1e-16). What changed is arithmetic ordering inside the sampler, not the draws.

Posterior statistics are correspondingly unchanged — per-transcript means and SDs agree to displayed precision:

```
transcript         mean(old)   mean(new)  Δmean/sd    sd(old)    sd(new)
NM_022658            4872.56     4872.56     0.000      50.31      50.31
NM_174914            1370.50     1370.50     0.000      62.92      62.92
NM_173860             961.02      961.02     0.000      30.42      30.42
...  (all 15 transcripts: Δmean/sd = 0.000)
```

against a Monte-Carlo standard error of 0.062 SD at n=256.

**So no release-note caveat is needed** — the exact-reproducibility property of bootstrap and Gibbs output is preserved, not merely its statistical properties.

## Validation

`cargo test --workspace --release`: 27 binaries, 0 failures. `cargo fmt --check` clean. Clippy at the 9 pre-existing warnings.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01R5jNNvJnFRiu2eC1JZAu2T

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `703c871abdf2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
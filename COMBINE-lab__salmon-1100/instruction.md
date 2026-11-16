# Issue

**Title:** perf(infer): build the packed CSR layout once per run

## Description

Part of #1092. .

**Measured: peak RSS −1.39% (plain), throughput null.** The larger half of this PR's original rationale was wrong; corrected below.

### What it changes

`optimize` and `optimize_with_init` each construct a `PackedEqClasses` internally, so a bias-corrected run built the flat CSR layout twice and a run with bootstrap or Gibbs three times. The three drivers (reads, alignment, RAD) now build it once and call `optimize_packed_with_init` directly; `refresh_combined` patches the combined weights in place after bias correction, since that is the only array `update_eff_lengths` changes. It asserts the class set has not changed, which holds because nothing ever clears `TranscriptGroup::valid`.

Also gates the raw `weights` array, which only the Gibbs sampler reads: `from_collapsed_with(.., keep_weights)` lets the drivers skip populating it.

### Correction to the original rationale

I claimed avoiding the rebuilds would cut peak memory. **It cannot.** `optimize()` builds its layout, uses it, and drops it on return, so two copies never coexist. The repeated construction costs allocation and copying, not peak RSS. That was wrong and I only found it by measuring.

What the measurement does show is the `keep_weights` gate working, and nothing else:

| configuration | develop | this PR | delta |
| --- | --- | --- | --- |
| plain, `-p 8` | 1079 MB | 1064 MB | **−1.39%** |
| `--numGibbsSamples 4`, `-p 8` | 1072 MB | 1082 MB | +0.89% (noise) |

~15 MB, only when Gibbs is off — which is exactly right, since `weights` is 8 bytes per CSR incidence and Gibbs is the only consumer. With Gibbs requested it is populated in both builds and there is nothing to save.

Wall clock over the same runs: 34.33s vs 34.59s. **No throughput change**, consistent with every other measured item in #1092.

10M read pairs from ERR188044, GRCh38 cDNA release-110 (207,249 transcripts), 16-core arm64, interleaved with the warm-up round discarded.

### Why take it anyway

- Building the structure once instead of three times is simpler to follow than three call sites that each rebuild it implicitly, whatever it costs.
- `refresh_combined` states what actually changes after bias correction, where the previous code re-derived everything and left the reader to work out that only `combined` differs.
- The `keep_weights` gate is a real if modest saving, and it makes the Gibbs-only lifetime of that array explicit rather than implicit.

If the memory number is too small to be worth the diff, that is a fair call and I will not argue it.

### Parity

Byte-identical to develop on `sample_data`: reads mode plain / all three bias models / `--numBootstraps 8` / `--numGibbsSamples 8` (including `bootstraps.gz`, which is what exercises the `keep_weights` gate) / bias+bootstrap; RAD requant plain / bias / Gibbs; alignment mode plain and bias+Gibbs at `-p 1`.

Alignment mode is pinned to `-p 1` because it does not reproduce run to run at `-p > 1` on develop either (#1098). Per the methodology note on #1092, byte comparison above `-p 1` cannot establish parity here.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab6870d9fd97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
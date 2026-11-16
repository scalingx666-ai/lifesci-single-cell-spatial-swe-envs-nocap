# Issue

**Title:** perf(quant): take the fragment-length snapshot once per batch

## Description

Part of #1092. .

**This PR is justified on determinism and code structure, not on throughput. Measured at scale, it makes no measurable throughput difference at any thread count.** The numbers are below.

### What it changes

`record()` runs once per fragment and began by taking its own fragment-length snapshot:

```rust
let fld_pmf = sh.fld.online_snapshot();
let fld_cmf = sh.fld.online_cmf_snapshot();
```

Both fields are `RwLock<Arc<Vec<f64>>>`, so that is two lock acquisitions and two `Arc` refcount round trips per fragment, on cache lines shared by every worker.

The snapshot is only replaced by `refresh_online()`, which runs once per mini-batch in `on_batch_complete`, so it is invariant across a batch. This takes it once at the top of each batch loop and passes it in.

### The semantic change, stated plainly

This is **not** a pure reordering of the same arithmetic. Previously a fragment late in a batch could pick up a snapshot that another thread had refreshed mid-batch; now every fragment in a batch uses the batch-start snapshot. **Fragments therefore use a uniformly staler FLD than before.** That changes what the fragment-length term means for a given fragment.

Consequently `quant.sf` is byte-identical to develop at `-p 1` **and nowhere else**. At higher thread counts there is a systematic shift, measured by the maintainers at 222–243 max TPM difference at `-p 32` against a 21–37 noise floor — small in context (r = 0.999986) and in the better direction, but real and not noise.

### Why it is still worth doing

It strengthens the invariant the per-fragment snapshot was introduced for in `4a25b3db` ("consistent FLD reads so duplicate transcripts stay symmetric"), rather than weakening it: previously two fragments in the same batch could see different snapshots, and now they cannot.

That shows up directly as reproducibility. Run-to-run spread of each binary against **itself**, 4 interleaved reps, max TPM difference over 207,249 transcripts:

| p | develop | this PR |
| --- | --- | --- |
| 1 | 0.000 | 0.000 |
| 8 | 9.656 | 7.284 |
| 16 | **42.296** | **7.094** |

**6.0x tighter at `-p 16`.** The maintainers independently measured 7x at `-p 32` on different hardware.

### Throughput: no change

Interleaved, 4 rounds, median wall clock against develop. 10M read pairs from ERR188044, GRCh38 cDNA release-110 (207,249 transcripts), 16-core Apple Silicon:

| p | develop | this PR | delta |
| --- | --- | --- | --- |
| 1 | 222.77s | 222.84s | +0.03% |
| 8 | 35.21s | 36.92s | +4.9% |
| 16 | 28.07s | 27.27s | −2.8% |

The p=8 and p=16 figures swing in both directions depending on which rounds are used (rounds 3–4, machine settled: +0.3% and −5.0%), which means they measure the machine, not the code. User CPU tracks wall throughout. Peak RSS flat.

**The original rationale for this PR — six atomic read-modify-writes per fragment collapsing to six per batch — does not materialise as throughput.** It was asserted from first principles and the measurement does not support it. Maintainer measurement at `-p 32` agrees.

A ~3.5% `-p 1` regression was observed by the maintainers on x86-64; it does not reproduce on arm64 (+0.03% wall, +0.07% user, interleaved). A plausible mechanism for the asymmetry: `record` gained two `&[f64]` parameters, and a slice is two registers where `&Arc<Vec<f64>>` is one, so this adds four register-equivalents to a per-fragment call — which x86-64 SysV (six register args) feels and AArch64 (eight) may absorb. Bundling the pair into one `&FldSnapshot` would restore a single register if that is worth closing off.

### Benchmark methodology

All timings interleave the binaries, rotating every round. A first blocked sweep (develop, then this PR, then #1099 back to back) produced an apparent +13%/+21% regression for whichever ran last, entirely from thermal drift; interleaving removed it completely.

Byte-comparison alone cannot settle parity here, because **develop is not run-to-run deterministic at fixed thread count** in the default path — see the noise-floor table above. Every cross-binary number is reported against that measured floor.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab6870d9fd97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
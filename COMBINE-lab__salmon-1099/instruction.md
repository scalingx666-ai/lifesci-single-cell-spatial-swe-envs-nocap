# Issue

**Title:** perf(quant): per-worker counters and reusable buffers in the fragment path

## Description

Part of #1092. , and the `record()` half of #1085.

**Stacked on #1095.** Justified on allocation and structure, **not on throughput**: measured at scale it makes no measurable throughput difference at any thread count. Numbers below.

### Per-worker counters

Six of the seven shared counters (`num_mapped`, `num_orphan`, `num_decoy`, `num_dovetail`, `num_frags_filtered_vm`, `num_below_threshold_vm`) were `fetch_add` on `AtomicU64`s shared by every worker. They are now plain `u64` on the worker, folded into the shared atomics once in `on_thread_complete`, where the bias models already merge.

`num_processed` deliberately stays shared: it is also *read* on the hot path to gate `use_aux`, so thread-localising it would change which fragments see the auxiliary model, and therefore the output. That is the #1084/#1089 ordering constraint.

### Reusable buffers in `record()`

Five throwaway `Vec`s per fragment (compatible mappings, online-posterior inputs, bias weights, per-mapping fragment-length terms, tid/weight pairs) move into a worker-owned `RecordScratch`. Only `tids` and `weights` stay fresh, since they are moved into the equivalence-class builder.

`compat` holds **indices** into `placements` rather than references, so the buffer can outlive a fragment.

### Two index spaces, now type-checked

That renumbering introduced a real hazard: `bias_w` is indexed by position within `compat`, not by placement index, and the two coincide only when nothing is strand-filtered. I got it wrong first time (caught by an unused-variable warning); it would have mis-weighted GC and positional bias on **stranded libraries specifically**, silently.

`ae61096` (maintainer) makes that unrepresentable rather than merely commented, with `MapIdx` / `CompatIdx` / `CompatAligned<T>`. Reverting to the original mistake now fails to build. Converting also surfaced that `online_post` is compat-aligned *and* read under a different guard than `bias_w`, which review had not caught.

### Throughput: no change

Interleaved, 4 rounds, median wall against develop. 10M read pairs from ERR188044, GRCh38 cDNA release-110 (207,249 transcripts), 16-core Apple Silicon, built from `ae610967`:

| p | develop | this PR | delta |
| --- | --- | --- | --- |
| 1 | 222.77s | 220.01s | −1.24% |
| 8 | 35.21s | 34.85s | −1.0% |
| 16 | 28.07s | 27.39s | −2.4% |

User CPU tracks wall. Consistently a hair on the fast side but inside run-to-run variation, so **no throughput claim is made**. The atomic-traffic rationale does not materialise as throughput, matching the same finding on #1095.

### Determinism and parity

Run-to-run spread against itself, 4 interleaved reps, max TPM difference:

| p | develop | this PR |
| --- | --- | --- |
| 1 | 0.000 | 0.000 |
| 8 | 9.656 | 6.600 |
| 16 | 42.296 | 10.775 |

Inherited from #1095 rather than added here.

Against develop: byte-identical at `-p 1`. At `-p 8`/`-p 16` the difference (5.6 / 28.6) sits below develop's own noise floor on this machine, so it cannot be resolved here; #1095 carries the parity caveat, since **develop is not run-to-run deterministic at fixed thread count** and the staleness change originates there.

### Benchmark methodology

Timings interleave the binaries, rotating every round. A first blocked sweep made this PR look +13% at `-p 8` and +21% at `-p 16` purely because it ran last after an hour of load; interleaving removed all of it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4391c95e7de8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
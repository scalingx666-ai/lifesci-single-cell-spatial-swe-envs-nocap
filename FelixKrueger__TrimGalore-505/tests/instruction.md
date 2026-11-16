# Issue

**Title:** fix(poly): remove poly-G before poly-A, and say what --poly_a does not remove

## Description

Two changes that came out of #504, which turned out to be two different things. The reported symptom — poly-A surviving into the output of a 3'seq library — is the documented behaviour of a 3'-anchored scan meeting an A-run that has sequence behind it, and the poly-A page never said the scan was anchored, so there was no way to tell that from a bug. Investigating it turned up a genuine ordering bug that `dev` still has, which is unrelated to the report. Behaviour changes only on `--poly_a` runs: the stage is skipped entirely when the flag is off, which is the default and every CI validation step, so no pinned md5 moves (checked against a binary built from `dev` for SE, PE, `--clock` and `--hardtrim5`).

### The ordering bug

The poly-A scan walks inward from the 3' end and records a cut only where the running score is positive and the gate `errors*5 <= n-i` holds, so a terminal poly-G run blocks it: on `[insert][polyA][polyG]` the poly-A stage fails, poly-G then strips the G-run, and the tail is left exposed. Poly-G now runs first — `insert60+A40+G15` goes 115 → 60 bp, `insert40+A60+G20` 120 → 40, `insert60+A20+G20` 100 → 60.

R2 is unaffected: poly-T comes off the 5' end, poly-G off the 3', and the 5' gate `errors*5 <= i+1` is indexed from the 5' end, so a 3' truncation cannot move it. Measured over 46,012 reads across five fixtures plus degenerate cases, zero divergence. On R1 the collateral is 10 reads in 10,000 on `illumina_10K`, worst cut 16 bp.

The mirror arrangement `[insert][polyG][polyA]` now under-trims by the length of the G-run (60 → 75 bp constructed, 2–9 reads per 10,000 in the fixtures), since poly-G is blocked where poly-A was before. Accepted and pinned by a test: dark-cycle G-runs are terminal by construction, so that arrangement is not a real 2-colour read, and it leaves sequence in rather than deleting it.

Nothing exercised `--poly_a` above the unit level and all 11 `poly_a_trim_index` tests used a tail flush with the 3' end, so the blocked case was untested at every level. Seven `trim_read` cases now pin the order, `quality.rs` covers `3 ≤ n ≤ 10`, and `tests/integration_poly.rs` drives the binary for the same cases plus poly-G without poly-A and the `--2colour` path.

### What #504 turned out to be

An adapter match removes the match **and everything 3' of it**; the scan removes only a run that reaches the read's end. That is the whole difference, and it is why `-a "A{20}"` — which is what Perl v0.6.x's `--polyA` actually was — does what the reporter wants and `--poly_a` does not. On `illumina10K_with_polyA.fastq.gz` the scan leaves 0 reads ending in ≥5 A but 37 containing `A{20}` somewhere; `-a "A{20}"` leaves 0 of the latter.

Keeping the sequence beyond an A-run is deliberate: the genome carries genuine runs of ten or more A's, so removing a run together with whatever follows depletes reads from those loci, invisibly. Worst in bisulfite and EM-seq data, where G→A conversion manufactures A-tracts that were never poly-A — around 11.6% of 150 bp windows of a converted human genome carry a 12-A run (#180). So the docs now state the anchored behaviour outright, show it with a worked read, and document `-a "A{20}"` as the supported route for 3' counting assays, preferring `A{20}` over `A{10}` because the shorter form matches more genomic A-runs: on `illumina_10K`, `A{10}` removes 213,308 bp and drops 1,358 reads below `--length 20`, against 28,064 bp and 138 reads.

The migration notes were also wrong about v0.6.x in three ways, read against `0.6.10:trim_galore`. The adapter was `A{20}` with `T{150}` as `-a2` — `autodetect_polyA_type` returns a 10-mer, but the caller overwrites it two lines later with `extend_adapter_sequence("A",20)` in both branches (`:501-530`), so the 10-mer only picks the direction and never reaches Cutadapt; the `--help` text was accurate. The Cutadapt call carried no quality cutoff, so the mode expected already-trimmed input, though length filtering did apply (`:1243`). And it rewrote read IDs — whitespace to underscores on every read, plus `32:A:` / `_PolyA:32` on reads that lost bases (`:1206-1213`). The migration table had claimed v0.6.x has no poly-A trimming at all.

### Verification

824 tests (516 lib + 308 integration), `clippy --all-targets -D warnings` clean on a cold cache, `fmt --check` clean, docs site builds. Differential sweep with both poly flags on, before vs after, by read ID: `illumina_10K` 10 shorter / 2 longer, `BS-seq_10K_R1` 7 / 9, `SRR24766921_RRBS_R1` 15 / 5, worst cut 16 bp. `Total written (filtered)` byte-identical on three fixtures, so `bp_after_cutadapt` and #232 hold.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a71d9fff5789`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
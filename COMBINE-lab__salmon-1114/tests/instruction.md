# Issue

**Title:** perf(map): reuse the per-fragment raw mapping and revcomp buffers

## Description

.

Stacked on #1113 — please merge that first; the base here is
`perf/1085-map-side-allocs`, so this diff shows only the new work.

#1085 listed four hot-path allocations. #1113 handled the two that measured
(the per-fragment `AHashMap` in `finalize_mappings_counted_into` and the
per-call `AHashSet` in `best_per_target`, together −2.39%, t=−5.28, faster in
9/9 rounds). This PR closes out the rest, so nothing in the issue is left
undecided.

### What changed

`MapScratch` gathers the mapper's per-fragment buffers into one struct that a
worker allocates once and then refills for the rest of the run. The mapping
entry points take one scratch parameter instead of three.

| buffer | before | now |
| --- | --- | --- |
| `raw` | fresh `Vec` per fragment | reused; `finalize_mappings_counted_into` drains it |
| `revcomp` | one `Vec` per orphan candidate examined | reused via `revcomp_into` |
| `dedup` | already threaded through from #1113 | folded into `MapScratch` |

`finalize_mappings_counted_into` now takes `raw: &mut Vec<RawMapping>` and
leaves it empty on every return path — including the two decoy early-returns,
which previously just returned and now clear explicitly. A new test drives all
five paths (empty input, decoy-only, decoy-dominated, ordinary, hashed-dedup)
and asserts the buffer comes back empty; removing either `clear()` makes it
fail with the path named.

### Correctness

Byte-identical against the #1113 build: sample data plain / bias / sketch, and
10M human fragments at `-p 1` — `quant.sf`, the eq-class file, and the
`meta_info.json` counters.

### Performance — null

10M human fragments at `-p 16`, interleaved A/B against the #1113 build, ten
rounds with the warm-up discarded:

```
  #1113 base   28.025s  sd=0.202
  + this PR    27.945s  sd=0.142
  delta        -0.080s  (-0.29%)
  paired       t=-0.92   95% CI  -0.255 .. +0.094 s
  faster in 4/9 rounds
```

That is not a win. The allocations are real, but at this scale they are
invisible against the alignment work around them — the same result the other
structural allocation changes in this series produced, and the reason #1113
was worth separating out. I am keeping this only for the invariant it
establishes (a worker allocates its mapping buffers once), not on a
performance claim. Happy to drop it if you would rather not take a change that
does not measure.

### Deliberately not changed

**The per-read `candidates` `Vec`** (#1085 item 2).
`join_reads_and_filter(left: Vec<MappingCandidate>, right: Vec<MappingCandidate>, ..)`
takes both by value and *moves* candidates into the `JointMapping`s it returns.
Each `MappingCandidate` owns a `MemChain`, so retaining the caller's buffers
would require cloning those chains — more work than the allocation saves. This
is a design change to the pairing interface, not a buffer swap, so it is out of
scope here.

**`cfg.chain.clone()` per read.** A false positive: `ChainConfig` is plain
`Copy` scalars, so the clone is a stack copy of a few words with no allocation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `174d2d240607`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
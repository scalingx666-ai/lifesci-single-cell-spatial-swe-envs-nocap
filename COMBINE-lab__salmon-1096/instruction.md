# Issue

**Title:** perf(rad,map): remove per-fragment and per-probe allocations from the hot paths

## Description

Part of #1092.  and #1083.

**Justified on correctness and structure, not on throughput.** Measured at scale by the maintainers, both changes are flat. Numbers below.

### The `GapKind` fix is the part that earns this PR

Gap and flank scores come from *different* functions (`ksw2_gap_global` vs `ksw2_flank_extend`) over the same kind of byte pair, and were kept apart only by appending a `0`/`1` byte to the query key. That is correct solely because no ACGT base equals `0x00` or `0x01` — an unasserted assumption about read content guarding a silently-wrong-score failure mode. It is now an explicit `GapKind` field.

### Allocation removal

**Alignment cache.** `cached_gap_score` / `cached_flank_score` built their lookup key by copying both substrings into `Box<[u8]>` *before* asking whether the entry existed, so every probe cost two heap allocations and two frees — cache hits included. `hashbrown::HashTable` can be probed with the borrowed `(kind, query, target)` triple, so only a miss allocates now, and once instead of twice.

Measured hit rates on 10M paired reads, GRCh38 cDNA:

| cache | probes | hits | hit rate |
| --- | --- | --- | --- |
| gap | 5,044,438 | 4,550,348 | 90.2% |
| flank | 113,786,498 | 57,614,418 | 50.6% |

So the change removes roughly two allocations on each of ~62M hits. Worth noting the flank cache avoids ~57.6M DP calls per run and is probed 22:1 against the gap cache — I had earlier suggested, on the strength of a wrong in-code comment, that it might be near-useless and worth deleting. It is not. The comment is corrected in this PR with the measured numbers.

These caches are on the default (anchored) scoring path only: `--fullLengthAlignment` takes the whole-read `ksw2_align_score` branch and never reaches them (measured: zero probes).

**RAD grouping.** `process_rad_fragment` and `collect_bias_fragment` each built a `BTreeMap<u32, Vec<usize>>` per record to group a handful of placements by transcript — a map allocation, a tree node and a `Vec` per distinct transcript, plus one further temporary `Vec` per transcript purely to hand `logsumexp` a slice. Roughly `2n + 7` allocations per fragment. `RadFragment::placements` likewise returned a fresh `Vec` per record; it becomes `placements_into`.

### Throughput: no measurable change

| path | develop | this PR |
| --- | --- | --- |
| mapping (cache change), 3 runs | 22.04s | 21.83s |
| `--rad` requant (grouping change), 3 runs | 12.16s | 12.15s |

Both within noise. The `2n+7` allocations per fragment and the two allocations on each of ~62M cache hits are **not** where the time goes. The PR does not claim a throughput benefit.

### Parity

- `--rad` requant of a 10M-fragment RAD at `-p 1`: byte-identical. This is the check that matters for the grouping's ordering argument, on real data rather than `sample_data`'s 15 transcripts.
- `--seqBias --gcBias`: byte-identical.
- `sample_data`: byte-identical across plain / bias / `--softclip` / RAD write / RAD requant / RAD requant with bias.

The ordering property is load-bearing: `logsumexp` is a floating-point sum, so groups must come out in ascending tid order and placements must keep arrival order within a group. Follow-up commit `9a35c7e` (maintainer) restructures the grouping to hold each placement's data in one record rather than four hand-aligned parallel arrays, which removes the same class of index hazard that #1099 hit, and measured that a stable sort subsumes the `(tid, index)` permutation key (100% of fragments arrive already sorted, mean 6.8 placements per fragment).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11edb3924c80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
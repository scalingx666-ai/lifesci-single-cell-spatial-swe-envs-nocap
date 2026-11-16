# Issue

**Title:** fix(quant): assert orphan-ness, not a single shared mate status

## Description

.

`record` asserted that every surviving mapping of a fragment carries the same `MateStatus`. That is stronger than the invariant that actually holds, so **debug builds aborted** on any decoy-bearing index in selective-alignment paired mode.

### Root cause

When a fragment has no non-decoy concordant pair, the orphan-suppression `retain` in `map_read_pair_into` does not run. Mate 1 can then survive as a `PairedEndLeft` mapping on transcript A while mate 2 survives as a `PairedEndRight` on transcript B — two different statuses, both orphans.

I replaced the assertion with a probe recording the distinct status set per fragment, over 300,000 fragments (281,348 mapped) on a GRCh38 decoy index. There is exactly one violating shape:

```
    525  MIXEDSTATUS L+R
```

0.19% of fragments. No fragment ever mixes `PairedEndPaired` or `SingleEnd` with anything else.

### Release output was never affected

The only consumer at that site reads the status to classify orphan-versus-paired:

```rust
if matches!(compat[0].0.get(placements).status,
            MateStatus::PairedEndLeft | MateStatus::PairedEndRight) {
    counters.orphan += 1;
}
```

Both orphan statuses satisfy that test, so which one sorts first cannot change the count. Everywhere else the status is read per mapping (`m.status == PairedEndPaired` for the proper-pair term), not through `compat[0]`.

### The fix

Weakened the assertion to the property the code depends on — the surviving mappings agree on *orphan-ness* — and rewrote the comment, which claimed "all-paired or all-orphan" implies one shared status. It does not: "orphan" spans two statuses. The counting is now expressed through a single `is_orphan` closure so the assertion and the branch cannot drift apart.

### Verification

**Regression test** (`mates_orphaning_to_different_transcripts_are_one_orphan_fragment`) forces the case directly: each fragment's R1 is drawn from one transcript and R2 from another, so no concordant pair exists anywhere. Negative-controlled — restoring the old assertion makes it abort with `a fragment's surviving mappings must share one status`; it passes with the fix. Note the assertion is debug-only, so in CI's `--release` run the test only checks the counting; in a debug build it is the real check.

**Debug builds on the GRCh38 decoy index** (194 decoys, `first_decoy_index=532552`), 300k PE fragments — the first three previously aborted:

| mode | before | after |
| --- | --- | --- |
| plain | abort (16 threads) | completes |
| `--seqBias --gcBias` | abort | completes |
| `--allowDecoyOrphans` | abort | completes |
| `--sketch` | completes | completes |
| single-end | completes | completes |

**Release parity vs develop**, 1M PE fragments at `-p 1` on the same index: `quant.sf` and `eq_classes.txt.gz` byte-identical, and every `meta_info.json` counter identical — including `num_orphan` at 30,667 and `num_mapped` at 938,004, so the counter this code feeds is unchanged under real orphan traffic.

Found while verifying #1114 on a decoy index.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7f949fb3f2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
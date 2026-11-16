# Issue

**Title:** perf(map): hold reference sequences at two bits per base while mapping

## Description

Holds the reference sequences at two bits per base while mapping, which lowers peak RSS by about a third in selective alignment. `quant.sf` is byte-identical to `develop`, and the time is unchanged or slightly faster.

> **Maintainer edits (Nov 2):**
> - the word-at-a-time match now steps over runs, so references with a few `N` runs (every genome-decoy chromosome) keep the fast path;
> - each reference's range of runs is computed at load instead of searched on every `ref_view`;
> - the effective-length correction takes the transcript length, fixing a panic with `--online --posBias` (and the existing one with `--online --sketch --posBias`).
>
> Together these turned a 5–8% genome-decoy slowdown into a 2% speedup. x86 results are added below.

## Why
`refseq.bin` sits on the heap at one byte per base. It is the largest allocation of a selective-alignment run (1.46 GB of about 2.86 GB on muscle), and mapping only reads short windows of it.

This stays on the heap, unlike the `mmap` removed in #1261: the footprint is fixed at load and nothing is paged in lazily.

## Changes
- **Loading:** `SalmonIndex::load_with_opts` takes `RefseqLoad::{None, Bytes, Packed}`. `Packed` reads the file block by block across threads and packs each block straight into the final buffer, so one byte per base is never in memory. The index format is unchanged.
- **Other bytes:** anything two bits cannot hold (`N`, IUPAC codes, lowercase) is kept as sorted runs and restored on read.
- **`RefProvider`:** `ref_seq` becomes `ref_view`, which returns a `RefView` over either bytes or packed bases.
- **Alignment:** only the bases of each gap or flank are decoded, into a per-thread buffer.
- **MEM extension:** on packed references, bases are compared a 64-bit word at a time, and the bytes of a run one at a time.
- **Bias:** `--seqBias` and `--gcBias` read whole transcripts, so they keep `RefseqLoad::Bytes` and see no saving. This includes their mapping pass.

## Results
### x86 (AMD EPYC 9575F, pinned cores, Linux), `-p 16`, medians of 3

| | wall | peak RSS |
|---|---|---|
| Muscle SRR13638690, GENCODE v50 | 8.6 -> 8.3 s | 3.06 -> 1.97 GB |
| GEUVADIS ERR188044 (10M pairs), Ensembl cDNA | 9.6 -> 9.6 s | 1.35 -> 1.06 GB |
| GEUVADIS, Ensembl cDNA + GRCh38 genome decoy | 16.1 -> 15.7 s | 10.2 -> 7.25 GB |

### Apple Silicon (Benjamin's runs, before the edits)
`develop` -> this PR, selective alignment, `-p 16`, Apple Silicon, medians of 8 ABBA-ordered pairs, on a shared machine (load average about 21, so times are noisy):

| | peak RSS | peak footprint | wall | user CPU |
|---|---|---|---|---|
| Muscle SRR13638690, GENCODE v50 | 2.86 -> 1.86 GB | 2.68 -> 1.66 GB | 12.73 -> 12.61 s | 133.7 -> 132.1 s |
| Mouse hypothalamus, 10M pairs | 2.29 -> 1.59 GB | 2.20 -> 1.46 GB | 15.40 -> 15.57 s | 135.6 -> 136.9 s |

Instructions and cycles are steadier under that load (`-p 4`, 4 pairs):

| | instructions | cycles |
|---|---|---|
| Muscle, full sample | -0.4% | -0.5% |
| Hypothalamus, 2M pairs | +1.4% | +1.1% |

So the small hypothalamus sample does pay about 1%. This may be the fixed cost of packing at load, which a larger sample would dilute, but that isn't confirmed.

## Verification
- Tests (391), clippy and fmt pass. New tests compare `RefView` reads and the word-at-a-time matches against the source bytes, including across `N` runs, IUPAC codes and a run split between load blocks.
- On x86, `quant.sf` is identical to `develop` for muscle and GEUVADIS, with and without the GRCh38 genome decoy, at 8 and 16 threads, and with `--posBias --seqBias --gcBias`.
- `quant.sf` is byte-identical on both samples above.
- On a synthetic index with `N` runs, IUPAC codes and a decoy, with 2M mouse pairs at `-p 8`, `quant.sf` and sorted `--writeMappings` are identical with:
  - the default options;
  - `--softclip --recoverOrphans`;
  - `--fullLengthAlignment`;
  - `--recoverOrphans --softclipOverhangs`.
- On that index `quant.sf` is also identical with `--gcBias --seqBias`.

## Formerly untested
- **Linux/x86 and a real genome decoy:** measured above.
- **Soft-masked genomes:** not a concern. The index builder uppercases every sequence before writing `refseq.bin`, so lowercase never becomes a run; the GRCh38 decoy has 1,072 runs in all.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f70de74d5092`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
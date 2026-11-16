# Issue

**Title:** fix(index): a failed rebuild no longer destroys the existing index

## Description

## Problem

A failed `salmon index` could destroy the index it was meant to replace. `refseq.bin` was truncated before the input was even opened, so a mistyped FASTA path emptied the store while the old `info.json` and `index.ssi` stayed in place. The directory still looked like a valid index. The next `quant` loaded it, then panicked on a slice, and the error blamed the read files:

```
salmon index -t typo.fa -i existing_idx   # fails, as it should
ls -l existing_idx/refseq.bin             # 28562 bytes -> 0
salmon quant -i existing_idx ...          # "mapping failed: Thread join error"
```

A rebuild killed part-way, by a walltime limit for instance, is worse in principle: a partial store longer than the old offsets imply keeps every slice in range, so reads would align against the wrong bases with no error. That case comes from reading the code; it was not run.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit traced `build()` and saw the truncation happen before the input was read, then confirmed it with `sample_data.tgz` and a debug build, which gave the sizes and error above. Tracked in #1283 (finding 3).

## Fix

- `refseq.bin` is staged as `refseq.bin.partial` and renamed once the build has finished. A failure during preprocessing, which is where bad input fails, leaves the old index untouched.
- Once preprocessing succeeds, the old `info.json` is removed, and the new one is now written last, after the store. So `info.json` marks a complete index: a build that dies in between leaves a directory that refuses to load, not a mix of old and new files.
- `load_with_opts` checks the store against the index: `num_refs + 1` offsets, and a last offset equal to the file size. It checks the file itself, so it holds for both `RefseqLoad::Bytes` and `RefseqLoad::Packed`. `load_ref_seqs` already validated its table; this path did not.

## Limit

A failure after preprocessing, such as `-k 33`, which passes the option check and panics during the build, still costs the old index. It can no longer be mistaken for a good one, though. That check is a separate fix.

## Verification

With this PR, on `sample_data.tgz`:

| Step | Result |
| --- | --- |
| `salmon index -t typo.fa -i idx` | exit 1, `refseq.bin` stays 28562 bytes, no `.partial` left behind |
| `salmon quant -i idx ...` afterwards | exit 0 |
| `quant` after emptying `refseq.bin` by hand | `idx is damaged: refseq.bin does not match the index. Rebuild it with salmon index.` |

New tests: `failed_rebuild_keeps_the_existing_index` and `a_truncated_reference_store_is_refused`. `salmon-index` tests, clippy on `salmon-index`, and the CLI `input_validation` and `output_contract` tests pass. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
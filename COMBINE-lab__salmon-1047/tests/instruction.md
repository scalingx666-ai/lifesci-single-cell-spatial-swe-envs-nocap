# Issue

**Title:** docs(cli): clarify salmon quant --threads help (auxiliary I/O thread, #993)

## Description

## What

`salmon quant` runs one auxiliary thread for FASTQ parsing/decompression on top of the `-p N` worker threads, so total CPU use slightly exceeds `-p` (e.g. ~1100% in `top` for `-p 10`). This surprised a user on an HPC scheduler that kills jobs exceeding their core allocation (#993).

This reword spells that out in the quant `--threads` help text and points HPC users to request one extra core.

## Change

A single doc-comment on the **quant** `--threads` arg. The `index` `--threads` is left unchanged (it reads a FASTA, not FASTQ, so the auxiliary-parser note doesn't apply there).

After:

```
-p, --threads <THREADS>
    Worker threads (0 = all cores). salmon also runs one auxiliary thread for
    FASTQ parsing/decompression, so total CPU use can slightly exceed this
    value; on schedulers that enforce the limit, request one extra core.
```

Docs-only; no behavior change.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54cdd903162f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
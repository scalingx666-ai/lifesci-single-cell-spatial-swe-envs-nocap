# Issue

**Title:** fix(cli): check the --phred64 claim against the input under --fastqc

## Description

`--phred64` describes the input and nothing verified it. Declaring the encoding to the bundled FastQC engine (#530) gave the mistake a detector, but a late one: FastQC refuses a file holding any quality character below ASCII 64, and it does so after the trimmed output and both trimming reports are already on disk, which leaves a successful trim sitting behind a non-zero exit. Under `--clump_only`, which does no quality arithmetic, nothing masked it at all.

A Phred+64 file cannot hold a character below ASCII 64, because Q0 *is* ASCII 64, so the input settles the claim on its own. This scans the first 10,000 reads of every input and the `--passthrough` carrier, and refuses before `ensure_output_dir` runs — naming the flag, the offending character and the likely cause:

```
Error: --phred64 declares Phred+64 input, but test_files/BS-seq_10K_R1.fastq.gz
contains quality character '?' (ASCII 63) within the first 10000 reads. A
Phred+64 file cannot hold anything below ASCII 64, so this input is most likely
Phred+33 — running it with --phred64 would reduce every score by 31. Drop
--phred64 if that is the case.
```

Deliberately scoped to `--fastqc`. `--phred64` on its own keeps today's behaviour — degraded output plus the startup NOTE — because refusing there would also reject `--hardtrim5/3` and `--clump_only` runs that pass the scores through untouched, and that is a wider behaviour change than a point fix should make. #532 keeps that question open.

The bound is a real limit, not a formality: a file whose only sub-64 character sits past the first 10,000 reads still fails inside FastQC, so this narrows the window rather than closing it. Three new tests cover the refusal (asserting nothing is written), the `--fastqc`-less scope, and a genuine Phred+64 file still passing. Both obvious mutants are caught — removing the guard fails the refusal test, dropping the `--fastqc` condition fails the scope test.

833 tests, cold `clippy --all-targets -D warnings` clean, `fmt` clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4b67eeddd07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
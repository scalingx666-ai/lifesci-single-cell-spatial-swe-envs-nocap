# Issue

**Title:** feat(io): read FASTQ and reference FASTA from streams

## Description

## Purpose

Lets `salmon quant` and `salmon index` read their inputs from a FIFO or process substitution.

This came up re-quantifying a 71-sample, 720 GB GEO series: streaming was the plan, and salmon 2.10.0 refused it.

```
$ salmon quant -i idx -l A -o q -1 <(cat r1.fq) -2 <(cat r2.fq)
Error: Illegal seek (os error 29)
$ salmon quant -i idx -l A -o q -1 <(gzip -c r1.fq) -2 <(gzip -c r2.fq)
opening /dev/fd/11: Invalid start character (æ), expected either '>' or '@'
$ salmon index -t <(cat txome.fa) -i idx
Failed to read the first two bytes. Is the file empty?
```

> **Maintainer edits (Nov 2):**
> - truncation detection moved from salmon's preflight into the FASTQ reader;
> - `index` reads each stream once instead of spooling it to disk;
> - the ENA script is dropped.
>
> The description below is updated to match.

## Changes

**`quant`.** salmon checked every uncompressed FASTQ for truncation in a separate pass before mapping. On a pipe, that pass took the first bytes. It existed because the FASTQ reader (paraseq) dropped a final record cut one or two lines in without an error. The pass is gone, and the check is in the reader:
- **paraseq-temp 0.6.3-pre.1:**
  - It fails on any non-blank bytes left after the last complete record at end of input, and on a final newline-less record that does not validate.
  - It fails on the fill that reaches the cut, so paired inputs report the cut rather than a mismatch in record counts.
  - Format errors can name their input.
  - These changes are offered upstream. piscem-rs 0.12.3 moves to it (COMBINE-lab/piscem-rs#19).
- **Readers are named after their paths.** A stream's name also carries the option it was given to, as in `/dev/fd/62 (-2)`.
- **Plain FASTQ runs read their input once.** On two 2.2 GB files at 16 threads, a run takes 9.4 s instead of 10.4 s.

**`index`.** A build opened each reference up to three times: to sniff its compression, to preprocess it, and to hash it on a separate thread.
- A non-regular input is opened once, and needletail detects its compression from the stream.
- When any input is a stream, preprocessing feeds the hashing from the batches it hands its writers, so each input is read once.
- Regular files keep their separate hashing pass, which overlaps the build. File builds are unchanged in time and peak memory.

**Docs.** The CLI reference has a "Reading from streams" section.

## Limits

- A plain stream cut exactly between two records cannot be told from a complete one. Where the source states the read count (ENA's `read_count`), compare it with `num_processed`.
- A stream is decoded serially, since the parallel gzip decoder needs a seekable file.
- Salmon's default two-phase mode still writes its intermediate RAD to the output directory during a run. The free-space preflight cannot estimate it for a stream, since it sees 0 bytes.

## Testing

- `cargo test --release --workspace`: 392 passed. Clippy and fmt are clean. New tests in `crates/salmon-cli/tests/input_validation.rs`:
  - a plain and a gzip FIFO give a `quant.sf` identical to the file;
  - a cut gzip stream is refused;
  - a plain stream cut mid-record is refused, and the error names the input;
  - 1, 2 and 3 orphaned lines are refused, and the error names the file; a trailing blank line is accepted;
  - `index` over a plain and a gzip FIFO gives the same digests and `refseq.bin` as the file.
- Through FIFOs, `quant.sf` is identical to the file runs:
  - paired, single-end and multiple files per mate;
  - plain and gzip;
  - `--sketch` and `--writeMappings`.
- Indices from GENCODE v50, Ensembl cDNA and a GRCh38 genome-decoy gentrome are file-for-file identical to `develop`'s, from files and from FIFOs (for the decoy, `-d` too).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f70de74d5092`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
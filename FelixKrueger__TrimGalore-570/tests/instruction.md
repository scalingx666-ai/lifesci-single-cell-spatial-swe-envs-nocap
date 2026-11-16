# Issue

**Title:** docs(threading): scope the N+4 thread model to FASTQ input; uBAM input runs 2N+4

## Description

.

As the issue suggests, this is a docs-only fix: the N+4 claim now applies only to FASTQ input, and the uBAM-input cost is written down where the N+4 claim appears. No code changes.

### What the thread count really is on `dev`

Measured on `dev` @ d862f7d (macOS), as the peak of `ps -M <pid>` sampled every 20 ms. The input was 600k reads (BS-seq_10K ×60), converted to uBAM with `samtools import`. FASTQ output was used so the output-side BGZF pool that #569 removes doesn't affect the numbers.

| Input | `--cores 1` | 2 | 4 | 8 | Model |
|---|--:|--:|--:|--:|---|
| FASTQ, paired | – | – | 8 | 12 | N+4 (as documented) |
| FASTQ, single-end | – | – | 7 | 11 | N+3 |
| uBAM, single-end | 1 | 8 | 12 | 20 | **2N+4** |
| uBAM, paired interleaved | 2 | 8 | 12 | 20 | **2N+4** |
| uBAM, two single-end files in one run | – | – | 12 | – | 2N+4 |

Breakdown for uBAM input: N trim workers, N conversion threads, 1 reader, 1 reorderer, 1 batcher and 1 main writer. The reader and reorderer replace the FASTQ decompressors.

The issue counted "N+2 per input file" and a "paired two-file" row (4N+7). Neither applies on `dev` any more:
- Two BAM files with `--paired` are refused, and so is a BAM paired with a FASTQ.
- Several single-end uBAMs are processed one after another.

So only one conversion pool exists at a time, and **2N+4 is the peak for any uBAM-input run**.

### Changes

- `src/cli.rs`: the `--cores` help text now says N+4 for FASTQ input and 2N+4 for uBAM input.
- `README.md`: the same in the feature list.
- `docs/.../performance/threading.md`:
  - The FASTQ breakdown block and prose are labelled as FASTQ-only.
  - The Perl comparison table is marked as FASTQ (the only input Perl 0.6.x accepted).
  - New **uBAM input** section with the 2N+4 breakdown.
  - The nf-core advice now says to pass half the allocation for uBAM input. 12 CPUs → `--cores 6` → 16 threads, the same as a FASTQ run at `--cores 12`.
- `docs/.../performance/benchmarks.md`: notes that the benchmark runs are FASTQ input and links to the uBAM section.
- `docs/.../reference/migration.md`: the Threads row adds "2N+4 for uBAM input".
- `CHANGELOG.md` and its docs copy (kept identical): one sentence added to the existing #529 entry.

Left unchanged, as the issue asked: `src/parallel.rs:76-81` (correct for the FASTQ path) and `docs/perf_data/clumpify-buckberry-2026-05-07/README.md` (a dated record).

### Ordering with #569

The figures assume #569 (#542) has landed. On `dev` today, uBAM *output* still adds the noodles `MultithreadedWriter` pool (N+1 threads): uBAM in plus uBAM out measured 17 at `--cores 4`, and paired FASTQ in plus uBAM out measured 13. #569 compresses in the existing workers and starts no new runtime threads, so after it, uBAM output matches FASTQ output and the numbers above hold. **Please merge #569 first.**

### Why no automated test pins the count

The count is only visible as a peak, sampled from outside a running process, and the `test_files/` fixtures finish in milliseconds. A test would be timing-dependent and flaky. Counting threads inside the test process doesn't work either, because `cargo test` runs tests in parallel. To reproduce the measurement:

```bash
trim_galore --cores 4 --paired pe.bam -o out & pid=$!
peak=0; while kill -0 $pid 2>/dev/null; do n=$(ps -M -p $pid | tail -n +2 | wc -l); [ $n -gt $peak ] && peak=$n; sleep 0.02; done; echo $peak
```

On Linux, use `ls /proc/$pid/task | wc -l` instead of `ps -M`.

### Checks

- `cargo fmt --all -- --check`: clean
- `cargo clippy --all-targets --release -- -D warnings`: clean
- `cargo test`: 876 passed, 0 failed (25 suites)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c014ca175a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
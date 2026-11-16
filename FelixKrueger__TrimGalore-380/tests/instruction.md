# Issue

**Title:** fix(input): reject non-restartable input with an accurate diagnostic

## Description

.

Trim Galore opens each input at least five times, so it cannot read a stream. Streams failed as though the user's data were at fault — `<(cat reads.fastq)` reported `doesn't seem to be in FastQ format`, a gzipped pipe reported `Failed to decompress first block`, and a named FIFO hung indefinitely with no message. All three now fail immediately, naming the constraint and giving the remedy. This is a diagnostic change, not a capability change: piped input did not work before and still does not.

Three layers, because no single check is sufficient:

- **`Cli::validate`** stats each path (replacing `exists()`, so no extra syscalls). Only this layer can diagnose a **writer-less FIFO**, because `fs::metadata` returns where `File::open` blocks forever.
- **`detect_input_format`** `fstat`s the handle it already holds, before the first `read`.
- **A second open** must start at offset 0 and return the same leading bytes.

`--passthrough` reached none of the format guards, so a stream there hung *after* the R1/R2 output files existed. It now passes through the guard, and a uBAM passthrough is rejected up front instead of failing mid-run with `stream did not contain valid UTF-8`.

Two smaller behaviour changes: a pipe or FIFO `--demux` barcode file is now rejected (read once, so restartability does not apply — but a writer-less FIFO blocked with no message *after* trimming and reporting had finished), and an empty FIFO reports as a pipe rather than as an empty file.

**Merge order:** ideally after #374, which touches the same two files. No overlapping hunks, so this is line shifts rather than conflicts — but #374 is an external contributor's and is green, so this branch should absorb the rebase.

<details>
<summary>Design rationale, verification, and what the reviews changed (AI-assisted)</summary>

Full record in `plans/08032026_reject-non-restartable-input/` — design, measurements with probe sources, two independent plan reviews, two independent code reviews, and a coverage audit.

**Both obvious guards were measured wrong.** A seekability probe — what the issue proposes — accepts `/dev/stdin` redirected from a regular file: that fd *is* seekable and still does not restart, because opening `/dev/fd/N` is `dup` on Darwin and shares the offset. A file-type check cannot replace the second-open test either, since that same input `stat`s as a regular file. And the byte comparison cannot stand alone: its own second open blocks forever on a FIFO whose writer has exited, which is the commonest FIFO shape (`mkfifo f; cat reads.fq > f &`).

Interrogating the **second** handle's start offset, rather than probing the first for seekability, makes the check exact rather than heuristic, and retires the residual where a stream repeating its first four bytes would defeat a byte comparison.

**Test discipline.** A test that opens a writer-less FIFO blocks rather than fails, which reads as a slow job rather than a red X. So every FIFO test bounds itself in-process (`timeout(1)` exists on neither Darwin nor `macos-latest`), the integration tests `spawn`-and-`kill` rather than use `Command::output()` (which cannot be interrupted), and the job now carries `timeout-minutes` plus a nextest `terminate-after`. Proven rather than assumed: forcing the type check to return `false` makes the FIFO test **fail in 10 s** with `blocked; it must fail, not hang`.

**Verification.** 470 tests pass; `fmt` and `clippy --all-targets --release -D warnings` clean. Output byte-identity confirmed against a build of the parent commit for SE-gz, SE-plain, and PE at `--cores 1` and `--cores 4`, each with a sentinel negative control. Byte-identity against Perl Trim Galore 0.6.11 could not be checked locally — **this PR's `Validate vs Perl TrimGalore` job is that check.**

**What review changed, three times.** Each revision was forced by the same class of error: a claim verified against a narrower set than it named.

| Stage | Finding |
|---|---|
| Before v1 | Seekability is a proxy for restartability, not the property itself. Measurement refuted it |
| Manual review of v1 | The byte comparison alone **hangs** on the commonest FIFO shape — a design defect recorded only as a test risk |
| Dual plan review of v2 | `--passthrough` was unguarded; the placement claim was stamped "Verified" against `cli.input` alone |
| Dual code review of v3 | The fix for that **regressed** `--passthrough <uBAM>` from a pre-output error to a deep failure leaving three empty files, on a justification the plan itself refuted two sections earlier |

Both reviewers at both stages independently found the same top finding.

**Known and deliberately not covered:** `trim_galore /dev/stdin` at an interactive terminal still waits for input (that is a terminal, not a pipe; telling them apart needs `isatty`), and an adapter FASTA given as `-a file:x.fa` is also read twice but is left unguarded as out of scope. Both recorded in the plan.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4703310e8ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
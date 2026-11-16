# Issue

**Title:** fix(io): publish an output only if its teardown succeeded

## Description

.

Three changes, one invariant: **an output file appears under its final name only if every
byte it owes was written.** #433 made the name appear only after the writer was closed;
this makes "closed" mean "complete".

### 1. The sink is an enum, so teardown is callable

`FastqWriter`'s `Box<dyn Write + Send>` becomes `Sink::{Plain, Gz, ParGz}` over
`BufWriter<File>`, `BufWriter<GzEncoder<File>>` and `ParCompress<'static, Gzip, File>` —
the shape the issue proposes. `finish()` runs the concrete teardown (`BufWriter::into_inner`,
`GzEncoder::try_finish`, `gzp::ZWriter::finish`) and returns its error **before**
`PendingOutput::commit`. A failed teardown returns with `pending` still armed, so its `Drop`
removes the temporary and nothing is published.

`impl Drop for FastqWriter` is gone rather than adapted: its only job was `let _ =
self.writer.flush()`, which `BufWriter`'s own `Drop` already does on the abandon path, and
removing it lets `finish` destructure `self` instead of the `Option`-take-then-`drop(self)`
dance the old signature needed. Field order still puts `writer` before `pending`, so on the
abandon path the compressor is closed before the temporary is removed — the reason the old
comment gave, unchanged.

`impl Write for Sink` forwards `write_all` explicitly, because `FastqRecord::write_to`
issues exactly one `write_all` per record and the default would wrap it in a loop over
`write`.

### 2. A single-end parallel worker error reaches the main thread

The result channel carries `Result<SingleBatchResult>`, matching the paired path; the worker
sends `Err(e)` where it printed `"Worker error: …"` and broke. The main loop keeps a
`first_error` and short-circuits on it. `drop(result_rx)` before the reader join is carried
over from the paired path for the same anti-deadlock reason its comment gives.

### 3. Both parallel paths join their workers before publishing

`thread::scope` joins workers on the way out of the closure — after the commit — so a
panicking worker committed a short output and only then re-raised, exiting 101. The joins go
after the reader join, where the reader has already dropped the work senders and every worker
is finished or about to be.

### Measured on this patch

| | result |
|---|---|
| `cargo test` | 16 suites, **708 passed, 0 failed** (440 lib + 268 integration) |
| `cargo fmt --all -- --check` | clean |
| `cargo clippy --all-targets --release -- -D warnings` | clean |
| decompressed output, before vs after | **identical md5**, `--cores 1` and `--cores 2` |

**Timing, and it does not settle the hot-loop question.** Two release builds of this
repository, differing only by this patch, alternating runs over 1M synthetic 100 bp
single-end reads at a 38% adapter rate, gzip output, on a 2-core VPS:

| `--cores 1` (the sink whose type changed) | median | min | max | n |
|---|---|---|---|---|
| `dev` @ `d2ea293` | 13.63 s | 13.20 s | 16.60 s | 10 |
| this patch | 14.12 s | 12.76 s | 17.79 s | 10 |

| `--cores 2` (`ParCompress`, unchanged path) | median | min | n |
|---|---|---|---|
| `dev` @ `d2ea293` | 9.50 s | 9.24 s | 3 |
| this patch | 10.16 s | 9.25 s | 3 |

The spread *within* each build is several times the gap *between* them, and the fastest and
the slowest run of the whole `--cores 1` set both belong to the patched build. **This box
cannot resolve a difference of this size** — it can say that nothing catastrophic happened
and no more. I am not claiming the swap is neutral or faster; if that claim matters for
merging, it wants a `scripts/benchmark.sh` run on hardware that is not a shared VPS.

Three unit tests in `src/fastq.rs` cover the new teardown path: a `Sink::Gz` over a
read-only `File` must return `Err` from `finish()` (the bytes that fail are exactly the ones
only `try_finish` writes), the same for a buffered `Sink::Plain`, and a positive control
asserting the trailer really is written — magic `1f 8b 08` at the head and eight zero bytes
of CRC/ISIZE at the tail.

### One behaviour change worth naming

**On the serial-gzip path the `.gz` bytes change.** The old teardown reached
`GzEncoder::flush`, which emits a deflate sync marker before the final block; `try_finish`
does not. Measured on the 1M-read output below: **101,067,014 bytes before, 101,067,003
after**, identical decompressed md5. `--cores N` output is byte-identical either way.

The `validation` job compares through `gzip -dc` and the two md5-stability checks in CI
(`sample_trimmed.fq.gz` re-run, clump-only determinism) compare a build against itself, so
nothing in CI should notice — but a `.gz` from this build will not md5-match one from
v2.3.0, and anyone holding such a hash downstream would.

### What this does not claim

- **The failure this fixes is not reproduced by a test.** The tests above prove the teardown
  error is propagated rather than discarded; they do not fill a disk. As the issue says, that
  needs a size-limited filesystem, and this patch does not add one.
- **(2) is a correctness fix, not a symptom fix.** Everything fallible in
  `process_single_batch` still writes into a `Vec`, so the path stays practically unreachable
  — the issue says so and I did not find a way to reach it either.
- **(3) is not directly tested.** Injecting a worker panic needs a test hook in the worker
  body, and adding one to a hot loop for this seemed worse than the argument.
- **The timing above is not `scripts/benchmark.sh`.** That wants the 84M-read Buckberry pair,
  `hyperfine`, and the `oxy` instance. This is 1M synthetic 100 bp reads at a 38% adapter rate
  on a 2-core VPS, wall-clock, alternating builds, 5 runs each — enough to catch a regression
  of the size a vtable-to-branch swap could cause, not enough to publish.

<details>
<summary>AI-assisted</summary>

This patch was written by an autonomous agent. Every claim above was executed on the
machine that wrote it rather than inferred: the test/fmt/clippy lines are real runs, the
before/after timing compares two release builds of this repository, and the gzip-framing
consequence was read out of `flate2`'s `gz/write.rs` (`flush` → `DeflateEncoder::flush`,
which `try_finish` does not call) and then confirmed against the two output files.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `115d84f3808c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
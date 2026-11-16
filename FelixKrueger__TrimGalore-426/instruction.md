# Issue

**Title:** fix(bam): refuse whitespace in read names and framing bytes in tag values

## Description

A uBAM whose read name contained whitespace was accepted, and the read-name tail plus every `--preserve-tags` aux tag were silently discarded — the FASTQ id is built as `@{QNAME}\tTAG:TYPE:VALUE` and re-split on the first whitespace, so a space in the name captured the tag tail. This refuses such records at the single BAM→FASTQ conversion point, which means **it also refuses FASTQ-output runs that previously succeeded**: a newline in a read name makes one record occupy five lines and desynchronises every record after it, so gating the check on output format would have closed a lost-tag hole and left a lost-file hole. Aux tag values get the same treatment through a second predicate (the read-name set minus space, which `Z`'s grammar makes legal), applied to whatever the tag emitter wrote so the `A` type is covered too. A mid-stream refusal can still leave a partial output file — that predates this change and applies to four other per-record bails, so it is asserted by a test rather than cured here, and tracked separately. 643 → 663 tests.

Addresses #415.

<details>
<summary>AI-assisted detail</summary>

**Why the check is read-side rather than gated on `--output-format ubam`.** The issue describes tag loss, which only happens on the uBAM-output path. But `FastqRecord::write_to` writes the id verbatim followed by a newline, so an LF inside a read name emits a five-line record — measured before the fix as 13 output lines for a 3-record input, at exit 0. That lands on the FASTQ-output path, where the reported defect does not reach. A character-class split (control bytes always, space/tab only for uBAM output) was priced and declined: input validity should not be discovered by changing an output flag.

**The reject set and why VT is excluded.** `u8::is_ascii_whitespace` — the bytes `parse_name_and_data`, `fastq::read_id_prefix` and the id's one-line framing treat as boundaries. VT (`0x0B`) is outside Rust's ASCII-whitespace set and is accepted by decision, not derivation: `append_to_id`'s `trim_end` uses Unicode `White_Space` and does strip a trailing one under `--rename` plus a clip flag. Rejecting VT read-side would over-reject files that work today, which is the same reasoning that admits `@` and non-ASCII. Those two still fail at noodles' record encoder on uBAM output with an opaque message — pre-existing, and worth its own issue.

**The `A` (Character) tag arm.** The scan runs over whatever `append_tag_type_and_value` appended rather than inside one match arm. An `A` value holding a newline reproduced the same corruption signature as the `Z` case, and on uBAM output Trim Galore itself emitted a spec-invalid `A` value — so `--preserve-tags` could produce malformed BAM, not merely malformed FASTQ.

**Why the fixtures place the offender past record 1.** Four entry points feed the conversion point and three run before the trimming loop: the sanity-check peek, adapter auto-detection (≤1M records) and the poly-G scan (≤1M). A single-record fixture is therefore always caught before any writer exists, so "nothing was written" holds vacuously and the writer-residue path stays untested. The cases run with `-a … --no_poly_g` to skip both pre-scans, which is the arm any file over 1M reads takes anyway. Each test names the entry point it pins.

**The partial-output residue.** The writer is created before the read loop, so a refusal past the pre-scan window leaves a partial file — and for uBAM the partial is valid, BGZF-EOF-terminated and samtools-readable, so nothing downstream flags it. The test asserts the EOF marker rather than mere non-emptiness, because indistinguishability from a complete BAM is what makes it a data-integrity problem. Not cured here: it applies equally to the aligned / reverse / secondary / supplementary bails, so the fix belongs across all five.

**Fixtures.** A newline inside a QNAME or a tag value cannot be expressed in SAM text, so samtools cannot build these; noodles' record encoder rejects the names too. But `bgzf::Writer` does no validation, so the records are packed by hand in `examples/mk_bam_fixture.rs` with only the framing from noodles — no external generator needed. All eight fixtures regenerate byte-identically from the recipes in `test_files/README.md`, and samtools reads all of them back with the expected records.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fc00f615297`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** fix(bam): make the uBAM path's normalization messages true

## Description

One IUPAC message served two opposite code paths and was wrong in both. On FASTQ→uBAM it announced "input uBAM … coerced to N **for FASTQ output**" — both halves backwards. On uBAM→uBAM the read-side message named a FASTQ output that does not exist on that run. Each direction now has its own text, and the read-side wording is output-neutral ("coerced to N on read"), which holds for uBAM→FASTQ and uBAM→uBAM alike.

The shared `OnceLock` was also a **reachable suppression bug**. A mixed FASTQ + uBAM single-end run reaches both call sites, and such runs are legal by design — `main.rs:296` offers "convert at least one input to uBAM" as a remedy. With the FASTQ file first, the user was told the wrong direction **and** never told about the genuine uBAM coercion, because the wrong message consumed the guard. Each direction now has its own static.

**New:** a once-per-run `NOTE:` when a FASTQ header description is dropped, echoing the text actually lost. BAM read names cannot contain whitespace, so everything after the first space goes — frequently the original instrument identifier or an Illumina `1:N:0:INDEX` field. Required by the format, never new, simply never disclosed. Nothing fires when nothing is dropped.

Also folded in: the output guide claimed uBAM records "round-trip losslessly" and `--output-format`'s help said nothing at all. Both now name the three FASTQ→uBAM normalizations (description dropped, bases uppercased, IUPAC coerced).

Five integration tests. Three fail against the unpatched tree; the byte-identity harness is still green, so output bytes are unchanged. 566 tests total.

<details>
<summary>AI-assisted: what the dual plan review corrected, and two fixture traps hit on the way</summary>

**Three of my original plan's claims were wrong**, and both reviewers reproduced them wrong independently on the built binary: (1) the "cross-direction suppression is nearly unreachable" argument, (2) "the read-side text is already correct", and (3) a drafted clause promising "Tab-separated TAG:TYPE:VALUE fields are preserved" — false on exactly the records that fire the notice, since a space *before* a tab discards the tags too. That clause is dropped rather than qualified.

Design decisions taken on evidence rather than taste: `NOTE:` over `WARNING:` because the tree has `WARNING:` ×10, `NOTE:` ×5, `Note:` ×0, and the sibling uBAM-path messages in the same register (format-mandated, non-actionable) all use `NOTE:`. Echoing the dropped text rather than naming `1:N:0:INDEX`, because what is lost varies — and per #408 it can be `--rename`'s own `:clip5:` annotation, which a user scanning for "instrument ID" would dismiss.

Two fixture traps hit while writing the tests, both caught only because the results were checked rather than assumed: my first `cargo test` filter matched **zero** tests and printed `test result: ok. 0 passed`, which reads like success; and my first fixtures were 8 bp reads, which the default `--length 20` filter discards *before* they reach the BAM writer — so no normalization happened and the tests failed for a reason unrelated to the code.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e00f323c5ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
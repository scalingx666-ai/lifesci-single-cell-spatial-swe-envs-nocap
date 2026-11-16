# Issue

**Title:** fix(cli): refuse --fastqc where no report is written, wire --fastqc_args

## Description

`--fastqc` was accepted and silently ignored on five dispatch arms — the run exited 0, wrote its normal output, produced no QC report and never mentioned FastQC, so a wrapper passing the flag unconditionally got no QC and no warning. Those five (`--hardtrim5`, `--hardtrim3`, `--clock`, `--implicon`, and paired FASTQ output from a single interleaved uBAM) reach no `fastqc::run` call site at all, and are now refused in `Cli::validate` rather than ignored. **Dual plan review found the same defect from the other side**, so it is fixed here too: the four `--clump_only` drivers took a `fastqc: bool` fed with bare `cli.fastqc`, which made `--fastqc_args` alone a silent no-op on a path that is otherwise capable. `Cli::fastqc_requested()` now carries that predicate once and is used at all ten sites, so `--fastqc_args`' documented "Implies --fastqc" is finally true everywhere. 663 → 684 tests.

Addresses #421.

<details>
<summary>AI-assisted detail</summary>

**Arm 5 needs the output format, not just the input shape.** `--paired --output-format ubam <one.bam>` routes *above* the interleaved-FASTQ arm into `run_ubam_output_paired_single_file`, which does run FastQC — `ci.yml:1173` and `tests/integration_ubam_out.rs:572` both assert it produces a report. A condition of `paired && input.len() == 1` alone would have refused a working feature and turned CI red. `--clump_only` is excluded so `main.rs:599`'s "requires two FASTQ input files" still wins, which names the actual remedy.

**Guard placement is load-bearing and took two attempts.** The block is the last fallible check in `validate`. Sited earlier it masks messages the user can act on — a malformed `--hardtrim5` value, an odd input count, a duplicated mate, a malformed `--adapter2` spec. The first implementation put it after the input-existence loop, which still masked the `--adapter2` parse error; that is pinned now by `malformed_adapter2_precedes_the_fastqc_refusal`. The principle is the one `main.rs:344-351` already argues: a malformed *value* reports before an unsupported *combination*.

**The gate was never uniform, which is what hid the sixth arm.** Five `main.rs` sites tested `cli.fastqc || cli.fastqc_args.is_some()`; five others passed bare `cli.fastqc` into the `--clump_only` drivers. The original plan asserted the disjunction held at all twelve call sites on the strength of grepping for `fastqc::run` — grep finds calls, not guards. The drivers' parameter is renamed `fastqc_requested`, because a parameter named `fastqc` is what invited `cli.fastqc` at the call site.

**#422's tripwire loses its FastQC allowance scoping**, which existed as a workaround for this defect (its own comment said so). The surviving rule — a FastQC-flagged run must write artefacts — is now unconditional across all 55 cases instead of being scoped away from five arms. Two new cases: one looping over every refused arm asserting non-zero exit, the message, and that nothing was written; and `clump_only_se_fastqc_args_only`, which puts the sixth arm under that rule. Reverting the five pass-throughs makes the latter fail with *"a FastQC flag is set but no FastQC artefact was written"* — the mechanism that missed the original defect now covers it.

**Verification.** Both code reviewers hunted specifically for over-rejection (the only way this change can do harm) and neither found an invocation that works on the base commit and now fails; one swept 16 invocations through a purpose-built binary. Nine mutations were designed against the guards and all nine go red. A coverage audit re-measured every claimed number, including reproducing both pre-fix defects on a binary it built from the unpatched base itself.

**Docs corrected in four places**, including a blanket "works on both FASTQ and uBAM output paths" promise, a report count that omitted `--passthrough`'s carrier report, and a `--help` remedy that offered `--output-format ubam` for four arms where it does nothing.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ffcef42f473`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
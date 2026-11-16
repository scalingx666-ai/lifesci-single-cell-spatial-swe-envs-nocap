# Issue

**Title:** fix(main): SE uBAM trim no longer destroys a report-named input

## Description

`trim_galore --output-format ubam sample.fastq sample.fastq_trimming_report.txt` overwrote input 2 with input 1's trimming report, then failed reading input 2 and reported that it was "not recognised as FASTQ" — an error describing damage the run had just caused. Verified: 40 reads in, 0 reads out, file replaced by a report. A user reading that error concludes they passed a bad file, not that theirs was destroyed.

The single-end uBAM arm planned only the primary `.bam` outputs, while `run_ubam_output_single` also writes `report_name` and `json_report_name`. Those never entered the candidate list, so the pre-flight's output-vs-input check couldn't see them. The single-end **FASTQ** twin was never exposed — it routes secondaries through `planned_secondary_outputs`, which the pre-flight does read. Fixed by adding both report paths to that arm's list, gated on `no_report_file` to match the writer (the #388/#391 shape).

Regression pair added, and the rejection test was confirmed to **fail against the unpatched tree** before the fix landed. 563 tests green.

<details>
<summary>AI-assisted: how this was found, and one deliberate non-choice</summary>

Found while planning #397 (pre-flight provenance), by probing the arms that change rather than reading them — five live probes against the built binary. Independently reproduced before filing.

I deliberately did **not** reuse `planned_secondary_outputs` here, even though it is the obvious helper: it interleaves reports per-input, so reusing it would reorder the FASTQ path's candidate list — and candidate order decides which path a collision message names, which existing tests rely on. Minimal shape chosen instead.

This is the **fifth** instance of the #383/#385/#388/#391 family, and worth stating plainly: a *missing* candidate is invisible to every guard currently in the tree, including the provenance typing #397 proposes (a type cannot detect an entry nobody wrote). The durable fix is deriving the candidate list and the writes from one source, or extending #391's exact-set assertion across all 11 pre-flight arms.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90dda11c1f58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
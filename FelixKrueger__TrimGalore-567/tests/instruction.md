# Issue

**Title:** fix(report): give --max_length its own line in the paired text report

## Description

`--max_length` removals had no line in the paired-end text report. The count was
accumulated on all three paths and written to the JSON, but never printed — and
once #561 made the length-cutoff line count only length removals, an over-length
pair was reported under no label at all. This adds the line, beside the
N-content one and following the same rule: emitted whether or not it rejected a
pair, so a parser sees a consistent shape.

Completes finding 5 of #546, whose second clause ("add a too-long line") #561
left out.

<details>
<summary>Detail (AI-assisted)</summary>

The report now reads:

```
Number of sequence pairs removed because at least one read was shorter than the length cutoff (…%):
Number of pairs removed for N content (…%):
Number of pairs removed for exceeding the maximum length (…%):
```

#546's reproduction for the original defect was a run reporting 9,997 "too
short" where the JSON held 4 too short, 6,841 too long and 3,152 discarded.

The `#233` comment above the unconditional emissions now covers both reasons
instead of naming N content alone.

`tests/integration_pe_report_removed.rs` already drives a four-pair fixture with
one over-length pair, so the new assertion is 1 at 25.00%, at both `--cores 1`
and `--cores 2`. Wiring the line to the N counter fails it. The module header
described the single-line behaviour and has been rewritten.

Still open, and not raised by the audit: `--discard_untrimmed` removals are
counted in `pairs_removed` but have no line of their own, so the text report
accounts for two of the three reasons.

Local: 872 tests pass, `cargo fmt --check` and `cargo clippy --all-targets -D
warnings` clean.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50b87a64a31f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
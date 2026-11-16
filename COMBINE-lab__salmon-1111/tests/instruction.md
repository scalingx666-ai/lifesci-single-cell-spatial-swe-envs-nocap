# Issue

**Title:** chore(deps): take libradicl 0.17 and let it own the tag-length limit

## Description

0.17 carries the two fixes we asked for upstream (COMBINE-lab/libradicl#50, PRs #51 and #52): an over-long tag value is bounded rather than allowed to wrap its length field and desynchronize the stream, and the `_reporting` writers return a `#[must_use]` outcome so a silent shortening has to be acknowledged.

## What changes here

With the format able to answer for itself, salmon stops restating the limit.

- `salmon_rad::MAX_FILE_TAG_STRING_LEN` — a `u16::MAX` this crate had no business knowing — is replaced by `salmon_rad::value_fits`, a pass-through to `TagValue::fits`
- the `@PG` bounding loop asks that instead of comparing against a hard-coded width
- the test asks it too, so it cannot drift from the format either

## Why the chain is still shortened here

Worth stating, since the upstream fix might look like it makes this redundant: libradicl bounds by **bytes**, which for a newline-joined `@PG` chain would cut a record in half and leave a line whose command is silently wrong. Dropping whole trailing records keeps every record that survives intact and truthful.

So the upstream fix is the **backstop** — it guarantees no producer can corrupt a file — and the record-wise shortening is the **mechanism** for this particular payload. They are not alternatives.

## Verification

- **RAD output is byte-identical** across the bump (same `md5` writing the same input under 0.16 and 0.17), so nothing about what salmon emits has moved
- full suite, `clippy --workspace --all-targets -D warnings` and fmt clean

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87cbb1a70a15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** fix(file_manager): add output-token truncation guards and append_file tool

## Description

## Summary

- **`write_file`**: hard-reject content > 12,000 chars; docstring now teaches the Two-Phase Write Protocol (scaffold → section fill → append for lists/bib)
- **`append_file`**: new tool for chunked appending with 6,000-char limit; designed for BibTeX batches (≤10 entries per call) and section streaming
- **`update_file`**: hard-reject `new_string` > 8,000 chars with guidance to split into smaller semantic units

## Root Cause

When an LLM generates a large file (LaTeX paper, BibTeX bibliography) in a single `write_file` or `update_file` call, the relay API truncates the output stream mid-JSON before the closing `"` or `}`, causing:

```
AnthropicException - Failed to parse tool call arguments: Unterminated string starting at line 1 column 15
```

This is **not** a context-window issue — it is an **output-token limit** on the relay. LaTeX/BibTeX content with `\\`, `\{`, and Unicode chars inflates JSON-encoded size ~1.5×, making truncation worse.

## Baseline Impact

Measured over 20 cases (2026-03-26 batch run):

| Metric | Value |
|--------|-------|
| Total cases | 20 |
| Full PDF output | 3 (15%) |
| Truncation errors confirmed | 5+ cases, at chars 66–140 |
| Cases where researcher not triggered (separate issue) | 4 |

The `write_file` truncation was the **single highest-frequency failure cause**.

## Validation

Controlled re-run after this fix (2026-03-30, same 7 general cases):

- **Case 1** (LaTeX review paper, 44 references): **FAIL → ✅ SUCCESS** — full 115K PDF compiled
- Agent read the Two-Phase Protocol from the docstring and adopted it proactively (0 `content_too_large` rejections — protocol followed before guard triggered)
- `append_file` was used correctly: bibliography written in 5 batches of ~9 entries each
- Remaining failures in other cases traced to `update_file` truncation (addressed in this PR) and a separate `think`-tool truncation issue (relay-layer, out of scope)

## Design Notes

- Guards are **in the tool layer**, not prompt-only — ensures coverage for General Team Leader which has no local prompt override
- Thresholds (12K / 8K / 6K chars) are conservative but leave room for realistic section sizes; can be tuned per deployment
- `append_file` requires the file to exist first, enforcing the scaffold-first mental model
- All three tools remain workspace-sandboxed via `_resolve_path`

🤖 Generated with [Claude Code](https://claude.ai/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c37a3c7d3c7c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
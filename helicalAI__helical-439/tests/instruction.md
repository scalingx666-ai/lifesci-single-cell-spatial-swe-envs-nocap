# Issue

**Title:** perf(transcriptformer): look up gene tokens once per batch call

## Description

## What

The Transcriptformer dataloader mapped every gene name of every cell through `np.vectorize`. Now the tokenizer maps the gene list once and indexes it with the batch's gene ids (`index=`). Tokens and the unknown-gene warning are unchanged.

## Checks

New tests in `ci/tests/test_transcriptformer/test_tokenizer.py` compare the tokens and the warning with the old lookup. One test drives `process_batch` with sorted genes. Breaking the call site fails it.

Version 3.1.4.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f190498b3497`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
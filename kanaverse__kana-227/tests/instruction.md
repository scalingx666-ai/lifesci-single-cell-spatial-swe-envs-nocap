# Issue

**Title:** Wait for transactions to actually complete in IndexedDB write operations.

## Description

- All `onerror` statements will now automatically `reject` with an appropriate error message.
- Removed helpers and just repeated the code in the relevant function bodies. This is desirable as IndexedDB operations are closely tied to the event loop and it helps to see that everything is happening in the expected sequence.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c4fa4632bba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
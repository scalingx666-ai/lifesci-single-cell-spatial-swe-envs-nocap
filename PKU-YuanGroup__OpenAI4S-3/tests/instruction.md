# Issue

**Title:** [codex] Fix annotation comment cancellation

## Description

## Summary

- Clear pending annotation comments from the composer immediately after they are submitted with a message.
- Add an inline cancel button to the pending comment chip so users can discard comments before submitting.
- Reuse one annotation deletion helper for pin popovers, pending-list removal, and the new cancel action.

## Why

Pending image comments could stay visible after submission while the message request was still running, and there was no direct cancel affordance on the composer chip if the user decided not to submit the comment.

## Validation

- `node --check openai4s/server/webui/app.js`
- `git diff --check`
- Direct annotation store/gateway assertion script

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0fd27c166ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
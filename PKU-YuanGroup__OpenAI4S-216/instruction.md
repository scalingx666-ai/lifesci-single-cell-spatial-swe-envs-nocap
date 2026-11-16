# Issue

**Title:** fix(ui): guard execution-history response ownership

## Description

## Summary

Prevent older execution-history responses from replacing newer cells. Track response ownership per frame, invalidate reads at snapshot and session/state/close boundaries, and guard error/loading cleanup and follow-on log reads. Independent frames retain valid cache entries, and failed reads remain retryable.

The contribution includes 17 additional execution unit cases and a real-gateway browser regression covering reversed response order, close/reopen, original source preservation and zero replay writes.

## Verification

Merge `c9d1ab3236b0bc89fb9b7450f58c2aeafe9c6f99` synchronizes the existing branch with upstream `e9f1c284ef5d73454b060847c67ec2f49015ac50`. All four original source/test/plan blobs are unchanged. Only generated-output conflicts required resolution through the official build; both test inventories preserve the upstream additions.

Fresh hosted-Linux validation in [cloud run 39629610029](https://github.com/dvd233/OpenAI4S/actions/runs/39629610029):

- **1,618 frontend tests in 147 files passed**.
- Both TypeScript projects and the official Vite build passed. A second build matched the staged distribution byte-for-byte.
- Bilingual documentation checks passed for 197 maintained directories and 1,997 direct files/assets.
- The actual contribution diff against the pinned upstream passes `git diff --check`; the result preserves the previous PR head and upstream as its two parents.

For exact head `c9d1ab3236b0bc89fb9b7450f58c2aeafe9c6f99`, upstream [CI](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39630227060) and [Protocol fuzzing](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39630227159) both completed successfully: **27 successful checks and 3 conditionally skipped nightly jobs**. This includes all four Python offline suites (3.10/3.12/3.13/3.14), frozen response shapes, pre-commit, Chromium/Firefox/WebKit workbench tests, Team/Stage-0 browser jobs and Linux sandbox checks. Skipped jobs are not claimed as executed.

The cloud preparation and upstream Linux checks are separate evidence; the preparation job did not rerun the Python suite or live browser itself.

## Reviewer focus and scope

Review `frontend/src/features/execution/exec.ts` for ownership and invalidation, its deferred-response tests, and `tests/browser_smoke.mjs` for the persisted-history regression. The existing R7/P1-04 evidence digest and its claim remain unchanged.

No backend API, kernel protocol, execution/replay behavior, dependency, permission or security boundary is changed. No tests were removed or weakened; default offline tests require no live model, cluster or credentials.

AI-assisted implementation and follow-up verification (GPT-6). This PR is open and non-Draft, awaiting human code-owner review; it has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9f1c284ef5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** fix(security): survive squash-rewritten fingerprints without widening a path rule

## Description

**Draft — this is step 1 of a deliberate two-step verification. Do not merge yet.**

## The problem

`Scan Git history` fails on `main` itself. The four findings are already-triaged synthetic fixtures, and `.gitleaksignore` already contains their exact `<file>:<rule>:<line>` triples — but with a **stale commit SHA**:

```
.gitleaksignore : 8d715ebe…:tests/test_model_profile_readiness.py:generic-api-key:80
CI reports      : f2d8adb1…:tests/test_model_profile_readiness.py:generic-api-key:80
```

`protect-main` permits only squash and rebase merges, so every branch that adds a suppression has its commits rewritten on the way into `main`, and the fingerprint that was correct on the branch names a commit that no longer exists. When #52 landed as a squash, four suppressions silently expired and the scan went red on a tree nobody had changed. This is structural: **fingerprint suppression is incompatible with squash-only merging**, and it will recur on every future suppression.

## Why not a path allowlist

The obvious fix — allowlist `tests/` — is one this repository has already argued against, in writing. From `tests/test_governance.py`:

> Suppressed by fingerprint rather than by widening a path rule, so a real leak in the same file is still caught, and pinned by count here so a new suppression cannot be added without a reviewer seeing it.

and from `tests/test_retrieval_source.py`, on why the canary is not exempted by being in a test file:

> a scanner that made an exception for test files would be a scanner with a hole exactly where people paste real keys "just to check".

So this PR does not widen a path. It moves the suppression from *"this finding, in this commit"* to *"this exact string, which is not a secret"* — `regexTarget = "secret"` with anchored patterns. That survives any rewrite of history, and gives up strictly less than a path rule: a real credential in these same files still fails the scan.

## Why this is a draft, and what step 2 will be

A `.gitleaks.toml` that gets `[extend] useDefault` wrong **replaces** the default rule set instead of extending it. The scan then finds nothing and exits 0 — which is indistinguishable from a scan that works. Landing the config and the allowlist in one commit would mean publishing "the secret scanner is green" with no evidence the scanner still has any rules. That is the failure mode this repo calls *wrong rather than absent*.

So:

- **Step 1 (this commit)** — the config lands with `[extend] useDefault = true` and **no allowlist at all**. The Gitleaks job on this PR must still report `leaks found: 4`. That is the evidence the default rule set is loaded.
- **Step 2 (next commit)** — add the allowlist, drop the four now-dead fingerprints from `.gitleaksignore`, and update the count assertion and comment in `tests/test_governance.py`. The drop from 4 to 0 is then attributable to the allowlist rather than to a neutered scanner.

Both run logs stay in this PR's history as the argument.

`--config` is also now passed explicitly rather than relying on gitleaks' auto-discovery, so a renamed or missing config is a loud error instead of a silent fallback to defaults.

## Not a real leak

For the record, both flagged values are synthetic: `abc123def456ghi789` is an obvious placeholder in a model-profile dict, and `Zx9Qw3Er7Ty1Ui5Op2As6Df4Gh8Jk0Lm` is a redaction-test canary that has to be high-entropy (the redaction under test keys on entropy) while not being provider-shaped (`scripts/source_secret_scan.py` correctly refuses `sk-…`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee4ae5425e1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
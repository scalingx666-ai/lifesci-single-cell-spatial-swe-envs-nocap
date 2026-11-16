# Issue

**Title:** fix: reject malformed null control counts

## Description

## Maintainer action required before merge

A maintainer must refresh the root `SHA256SUMS` entries for `kit/check_run.py` and `kit/tests/test_check_run.py` before merging. Both files are listed in that manifest, and their current checksums no longer match. `kit/SUBMIT.md` reserves root-manifest maintenance for maintainers. This PR intentionally changes only the parser and its regression tests; it does not modify the manifest.

## Bug and reproduction

`check_null` previously removed every non-digit character before converting `controls` to an integer. Consequently, `-400` and `4.00` both became `400` and incorrectly satisfied the minimum of 400 controls.

A `null_test.md` containing the following fields reproduces the acceptance error on upstream commit `7aca3835635e5323b48cdf3b5b59fcde502cab28`:

```text
controls: -400
best_control: 0.4
real: 0.9
real_beats_all_controls: yes
command: python3 null.py
```

Replacing the first value with `4.00` reproduces the same error. A local comparison of the baseline and proposed `check_null` functions using identical fixtures confirmed that `-400`, Unicode-minus `−400`, and `4.00` are accepted before the fix and rejected afterward. `399` is rejected by both versions; `400`, `401`, and a whitespace-trimmed `400` remain accepted.

## Fix

Validate the complete parsed value against `[0-9]+` before integer conversion. Reject malformed counts explicitly, while preserving the existing minimum-count check and ordinary integer behavior. Add regression coverage for valid, insufficient, and malformed counts. Existing AGPL notices are preserved.

## Checks actually performed

Verified proposed HEAD: `91419e28c801adb3c4b3fe92d7c50c56a543b237`.

On local Python 3.9.6:

- `python3 kit/tests/test_check_run.py`: **42 tests passed**, exit 0.
- `python3 -m py_compile kit/check_run.py kit/tests/test_check_run.py`: passed, exit 0.
- Baseline/fixed reproduction described above: all seven input comparisons matched the expected behavior.
- `git diff --check`: passed. The upstream-relative diff contains exactly the two files named above.
- Checked open upstream PRs immediately before submission: no existing analogous PR found.

GitHub Actions CI was not run in the fork for this HEAD. These are local verification results; no green CI is claimed. This is a mechanical validation fix, with no scientific-result claim, release, or merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7aca3835635e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
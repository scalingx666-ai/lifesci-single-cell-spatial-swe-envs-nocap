# Issue

**Title:** Fix mt.zscore swapping the KSEA and RoKAI flavors

## Description

`mt.zscore` applies the two flavors the wrong way round. With `flavor="KSEA"` the mean of all features is not subtracted, and with `flavor="RoKAI"` (the default) it is. This is the opposite of the docstring and of decoupler 1.x (`method_zscore.py`: `if flavor != 'RoKAI': mean_all = np.mean(m, axis=1)`). The branches appear to have been swapped in the 2.x port.

Minimal example (one source, targets = first three of six features, values 11, 12, 13, 10, 9, 8):

| flavor | expected (formula) | decoupler 2.3.0 |
|---|---|---|
| KSEA | 1.389 | 11.110 |
| RoKAI | 11.110 | 1.389 |

This PR swaps the two branches back, adds a test that checks both flavors against their formulas, and adds a CHANGELOG entry noting that scores from the default flavor change.

`pytest tests/mt/test_zscore.py`: the new test fails on `main` and passes with the fix; `pre-commit` passes on the changed files.

**LLM usage:** An LLM coding assistant helped find and draft this fix. I have reviewed, understood and tested every changed line.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6835a406c9e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
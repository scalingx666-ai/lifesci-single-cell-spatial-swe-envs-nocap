# Issue

**Title:** Enables reads to be processed before end of contig

## Description

As noted in #428, `get_bundle.start` was never updated. As such `get_bundles.check_output` only returned `do_output=True` at the end of a contig which is not the intended behaviour. This PR fixes this.

Note that this also changes the output order for some test files. For each of the test files modified herein, I have manually checked (`diff <(sort new_test_output) <(sort old_test_output)`) to make sure the only difference is the order of the output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `09ba49264a38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
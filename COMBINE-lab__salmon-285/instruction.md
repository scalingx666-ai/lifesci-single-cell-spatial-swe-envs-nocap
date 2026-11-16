# Issue

**Title:** Tweaks to CEL-Seq2 support for Alevin

## Description

A PR noting the differences in my approach to #269.
The one that I think needs addressing is in `writeFastq` (https://github.com/COMBINE-lab/salmon/compare/develop...PeteHaitch:develop?expand=1#diff-bf2f37cd9ea77a5c454a5bd860a924ee); without some change to this the `UMI` and `CB` are incorrectly extracted for CEL-Seq2. 
I simply commented out the original lines and modified it as needed for CEL-Seq2 in order to test my modified version.
I guess some sort of protocol-specific conditional is needed here.

The remainder are minor/cosmetic choices of variable names (please feel free to ignore!).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b15dcffaab5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
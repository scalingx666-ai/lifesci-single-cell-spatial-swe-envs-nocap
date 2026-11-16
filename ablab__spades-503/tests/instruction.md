# Issue

**Title:** Removed the second parse function (without check for allowed file types)

## Description

There are two functions with the same name (parse) and almost the same content in the module.

[The first function](https://github.com/bondarevts/spades/blob/8d13ac08916ca2612ece5e882fe0d8c21b76d359/assembler/src/spades_pipeline/common/SeqIO.py#L96-L101) is safer (it checks for allowed file types and fails early). It is never used because it's overridden by the second implementation.

I guess that [the second function](https://github.com/bondarevts/spades/blob/8d13ac08916ca2612ece5e882fe0d8c21b76d359/assembler/src/spades_pipeline/common/SeqIO.py#L125-L129) can be safely removed (if there are no calls with wrong arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a42abdbe7294`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
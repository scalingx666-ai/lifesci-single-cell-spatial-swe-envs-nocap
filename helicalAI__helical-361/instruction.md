# Issue

**Title:** replaced AutoTokenizer/AutoModelForMaskedLM with

## Description

direct imports of NicheformerTokenizer/NicheformerForMaskedLM, no trust_remote_code

TODO, solve mismatch of padding token:


tokenization_nicheformer.py -> PAD = 0 | MASK = 1
masking.py -> PAD = 1 | MASK = 0

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb80a76458e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
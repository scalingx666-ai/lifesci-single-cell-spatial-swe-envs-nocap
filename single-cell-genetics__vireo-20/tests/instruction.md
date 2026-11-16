# Issue

**Title:** Fixed error in output with --noDoublet & slice cells

## Description

Hi,

First of all thanks for developing Vireo (and cellsnp-lite), it's really a great tool that I use quite frequently in my work. Excellent job!

I have encountered a problem when running with the `--noDoublet` mode, and found the problem: You create a matrix of zeroes in the shape of ncells x possible donor combinations but you had ncells x all possible cell combinations in that line.
Furthermore I added an int() in that line because the division would return float values.

Additionally, I have been having some scipy matrix errors during donor deconvolution when running vireo on big datasets that are deeply covered (eg. 500,000 high quality variants x 50,000 cells). This can be avoided when running fewer cells, so for convenience I added a flag to run only a subset of the input cells:  `--cellRange`, eg. `--cellRange 0-10000` to run the first 10,000 cells in the cellSNP data.
This also helps to use less RAM!

Hope you find this useful and let me know if anything is unclear.

Best,
Christoph

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1dd455c4df0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
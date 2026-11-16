# Issue

**Title:** Add newlines to end of object definitions

## Description

This is a very minor commit to add newline characters to the end of some object definitions.

Previously, if we inspected an AnchorSet object in the console then we got:

An AnchorSet object containing <some number> anchors between the reference and query Seurat objects. 
 This can be used as input to TransferData.> 

i.e. the prompt is on the same line as the last line of the message. I presume that this is not deliberate? If it was deliberate then sorry for the pointless change! I made this change for objects with the TransferAnchorSet, IntegrationAnchorSet, ModalityWeights, and SCTModel signatures.

Thanks,
George

# Note

Thanks for your interest in contributing! Please make your PR to the `develop` branch. You can check out our [wiki](https://github.com/satijalab/seurat/wiki) for the current developers guide.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eaaf6750c8b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
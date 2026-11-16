# Issue

**Title:** Fix `HarmonyIntegration` deprecation warning

## Description

This PR updates `HarmonyIntegration` to avoid calling `harmony::HarmonyMatrix` in favor of `harmony::RunHarmony` since the former was deprecated in `harmony` v1.0.1. 

Additionally, since the `harmony::HarmonyMatrix` was deprecated, the following arguments passed in through `HarmonyIntegration` have been ignored: `tau`, `block.size`, `max.iter.cluster`, `epsilon.cluster`, and `epsilon.harmony`. The default values for these arguments were consistent between both packages except for `epsilon.harmony`—to avoid changing the default behavior of the `Seurat` interface, we've updated the default value to 0.01. If instead we'd like to keep the default value as is, then we'll need to adjust the expected values in our tests. 

Resolves:
- 
- 
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `855e6c9f311e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
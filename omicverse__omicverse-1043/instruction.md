# Issue

**Title:** Align SPLIT branch semantics and preserve CytoTRACE gene identifiers

## Description

Synchronize the embedded SPLIT receiver, residual-profile swap, missing-class and single-type status behavior with the standalone repair. Pass gene/cell identifiers into CytoTRACE so ERCC filtering and output provenance survive the AnnData adapter.

Validation: 12 focused tests passed on the rebased branch, covering existing SPLIT behavior plus receiver/shift semantics and CytoTRACE count/name forwarding. git diff --check passed. Existing pytest-asyncio configuration and AnnData deprecation warnings remain; no broader suite pass is claimed.

This PR changes neither package versions nor unrelated trajectory methods. Paired standalone-package and tutorial PRs are submitted separately.


## Related work and sequencing

Standalone SPLIT fix: 
Standalone CytoTRACE review:  (upstream disables forks; maintainer transfer is needed)
Paired tutorial: 
Review/release the CytoTRACE backend fix before promoting the tutorial as runnable with a released backend.


## Latest-main integration check (2026-11-13)

Validated a local combined tree based on upstream master 19bfb26d (2.4.3), the nine roadmap adapter PRs, #1035 and #1043. Adapter/RUVg/registry plus SPLIT/CytoTRACE focused tests: 49 passed, no skips. All six real standalone backend acceptance paths passed their existing R fixture gates. This validates the documented subsets; no package publication or broader biological equivalence is claimed. Existing pytest, AnnData and registry warnings remain.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df1a67889334`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
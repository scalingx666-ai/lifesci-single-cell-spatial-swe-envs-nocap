# Issue

**Title:** feat(single): add dynamo perturbation backend

## Description

## Summary

- add a lazy-loaded dynamo backend to `ov.single.perturb`, with KO/KD/OE, per-cell responses, native transitions, grouped rankings and optional KO velocities
- prepare missing PCA, dynamics, neighbors, embedding and vector-field prerequisites from velocity-compatible data
- support native expression levels and prepared custom PCA inputs, and reject known unsafe dynamo-release 1.5.3 combinations before perturbation
- document wrapper options, native parameter forwarding and downstream prerequisites in the public API; include the bilingual tutorials from

The default `j_delta_x` response uses the learned vector field's analytical Jacobian. Other methods retain their native definitions. Responses live in `delta_X` and the named layer; `.X` remains baseline expression, and this backend does not reconstruct a GRN. `group` and `vf_ko` are convenience interfaces rather than replacements for dynamo's complete ranking, KO-model and fate-integration APIs.

Local validation passed with 139 tests and no skips on dynamo-release 1.5.3. Ten full-reference-data comparisons covered all five perturbation methods, selected cells, explicit levels, custom PCA/Jacobian inputs and time scales; the maximum gene-response difference was zero. Native transition and embedding outputs also matched. Separate comparisons covered fp, pearson, cosine and kmc projections. Full raw-data KO/KD/OE fitting and existing backend regressions passed. Shared function-scoped fixtures keep test preparation consistent while preserving every parameter combination and assertion.

The 1.5.3 precomputed `delta_Y` failure, unsafe PCA/full-gene target-zeroing indices and transform projection's baseline-velocity behavior are handled explicitly rather than presented as supported scientific workflows. These checks establish numerical/interface parity on the reference data, not biological predictive accuracy.

The tutorial submodule points to the companion PR's commit; merge the tutorial PR before this PR. Updated English and Chinese tutorial pages passed targeted Sphinx builds and retained portable table outputs. No dependency changes or local validation artifacts are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af354858bfb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Resolve pathway selections to member genes

## Description

Selecting a pathway adds its name to plots as a feature instead of selecting its genes.
Cause: The comparative selection handler bypasses the existing pathway-to-gene resolver.
Coverage: a failing regression test now passes.

Pre-existing failures unrelated to this change, identical before and after: 58 (packages/config/src/VitessceAutoConfig.test.js, packages/config/src/VitessceConfig.test.js, packages/config/src/generate-config.test.js, packages/file-types/abstract/src/matrix-guard.test.js, packages/file-types/json/src/json-loaders/AnnotationStoryJson.test.js, packages/file-types/json/src/json-loaders/JsonLoader.test.js, packages/file-types/json/src/legacy-loaders/CellsJsonLoaders.test.js, packages/file-types/json/src/legacy-loaders/ClustersJsonLoaders.test.js, packages/file-types/json/src/legacy-loaders/GenesJsonLoaders.test.js, packages/file-types/json/src/legacy-loaders/MoleculesJsonLoaders.test.js, and 48 more)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fed671997074`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
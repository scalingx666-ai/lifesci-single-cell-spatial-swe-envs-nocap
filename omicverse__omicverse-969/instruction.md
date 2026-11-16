# Issue

**Title:** fix(space): enforce STAligner batch identity and actual alignment

## Description

Keep STAligner observation identities, expression matrices and spatial graphs aligned across both training stages. Shared barcodes require explicit or inferable batch identity; named graph edges are realigned after reordering, and both stages consume Batch_list.X in the combined gene order. Tensor graphs work without torch-sparse.

Preserve the original method's 500-epoch pretraining schedule, MNN graph traversal, first-positive selection and negative-sampling population (including possible self-negatives). Short runs must explicitly set pretrain_epochs. Seed model initialization and run the original implicit DataLoader sampler inside a scoped Torch RNG context: passing a separate Generator changes the upstream random draw sequence. NumPy RandomState is local, and the caller's Torch RNG state is restored.

Hnswlib approximate search remains the default; exact search requires mnn_approx=False. Explicit disconnected pair groups are accepted. No-anchor training and prediction before training remain errors. Combined rows must be contiguous by batch and match source order, allowing uniform concatenation suffixes.

Validation:
- 25 focused tests passed, including two-stage real CPU training, positional arguments, original schedule, MNN traversal, negative sampling, and upstream loader RNG consumption without leaking caller state.
- Direct comparison with unmodified zhoux85/STAligner commit 85ca4ce34072a37b949733aa55a3d3854ed89038 through train_STAligner_subgraph: 256 real DLPFC 151673 spots, 64 genes, identical expression/graphs, default [512,30] dimensions, 1000 epochs, knn=100, hnswlib, CPU. Seeds 666 and 7 each produced max absolute embedding difference 0 and RMSE 0.
- The real-data fixture divides one slice into two spatial halves for computational parity; it is not a biological batch-correction evaluation. Upstream set traversal depends on Python hash order, so this does not promise cross-process/platform or GPU bitwise equality.
- git diff --check passed. No CI or project dependency changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** perf: reduce GPU memory across RCTD fitting stages

## Description

## Summary

Large RCTD runs can keep both the complete spatial count matrix and all sigma likelihood tables on the GPU. This PR reduces their residency and IRWLS temporary allocations while preserving the existing numerical behavior.

- Full mode adds `run_rctd(..., mode="full", stream_gpu=True)`: counts and nUMI stay in host RAM and only the current batch is transferred. The resident path remains the default.
- Bulk platform-effect fitting reduces counts and nUMI on CPU without materializing a full long-double copy, then transfers only the reduced vector and scalar. Their original dtype is preserved.
- Sigma estimation stages and releases one Q/SQ pair at a time.
- Shared IRWLS reuses derivative workspaces in place and releases unused intermediates earlier.
- Documentation explains full-mode streaming and the optional `PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True` setting for allocator fragmentation.

The 0.4.0 automatic batch-size formula is unchanged, including when streaming is enabled. Set `batch_size` explicitly to control the streaming chunk size. `P` and `x_vals` retain defensive copies in Full and Sigma.

## Validation

Local environment: Python 3.13, PyTorch 2.14.1+cu130, NVIDIA RTX 5070.

- `pytest tests/ -q -m "not slow"`: 188 passed, 1 skipped, 16 deselected.
- `pytest tests/ -q -m slow`: 16 passed.
- Targeted Full-streaming and Sigma tests: 15 passed.
- CI-pinned Ruff 0.17.0: `ruff check src/ tests/ docs/` and `ruff format --check src/ tests/ docs/` passed.
- `sphinx-build -W --keep-going -n -b html docs docs/_build/html`: passed.
- `git diff --check`: passed.

The Full tests cover CPU/CUDA and float32/float64, including exact resident-versus-streamed equality with the real IRWLS solver at the same batch size and a CUDA allocation regression check. The Sigma test checks that unused tables are never staged and that each Q/SQ pair is released before another pair is loaded.

An AST comparison against `520350e` confirms that this review-cleanup commit changes no executable library logic beyond removing an unused import. The historical CHANGELOG from 0.4.0 downward matches upstream exactly.

## Real-data evidence

 reported bit-identical outputs after preserving the bulk sums' dtype. On the tested Visium HD workload, full-mode streaming reduced peak GPU memory from about 11 GB to about 1 GB at the same runtime. These are workload-specific measurements, not a newly rerun benchmark for the cleanup commit.

## Scope

Streaming is currently Python-only and Full-only; Doublet and Multi continue to stage their complete count matrices. The benchmark harness, automatic batch-size redesign, CLI streaming option, and Doublet/Multi streaming are outside this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `233db3fbcb22`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
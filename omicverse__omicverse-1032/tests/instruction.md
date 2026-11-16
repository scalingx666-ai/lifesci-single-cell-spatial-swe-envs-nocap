# Issue

**Title:** qc: fix NameError 'backend' in cpu-gpu-mixed mode (2.4.0 regression)

## Description

## Problem
In `ov.settings.cpu_gpu_mixed_init()` mode, `ov.pp.qc` on an in-memory AnnData fails with

```
NameError: name 'backend' is not defined   (omicverse/pp/_qc.py, qc_cpu_gpu_mixed)
```

`qc_cpu_gpu_mixed` passes `backend` to its cell/gene filters but never received it (regression from #1022, shipped in 2.4.0). AnnDataOOM inputs were not affected (they take the CPU OOM path), which is why the Fig. 4 mixed benchmark did not catch it; `tests/mcp/test_real_p0_pipeline.py` fails on master when an earlier test leaves the mode at cpu-gpu-mixed.

## Fix
`qc_cpu_gpu_mixed` takes `backend=None`; `qc` passes the resolved backend.

## Test
`tests/pp/test_qc_workflow.py::test_qc_cpu_gpu_mixed_in_memory_matches_cpu`: mixed-mode qc keeps exactly the same cells and genes as cpu mode (fails on master with the NameError). `tests/pp/test_qc_workflow.py` and `tests/mcp/test_real_p0_pipeline.py` pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3e41390f6eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
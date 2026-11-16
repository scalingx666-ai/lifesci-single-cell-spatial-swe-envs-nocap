# Issue

**Title:** feat(settings): support devices arg in cpu_gpu_mixed_init

## Description

## Summary

Implements #853. On a shared multi-GPU server, `cpu_gpu_mixed_init()` offered no way to choose which GPU the torch-backed mixed-mode kernels run on — it always used torch's current device (GPU 0). This adds a `devices` argument that mirrors the existing `gpu_init(devices=...)`:

```python
ov.settings.cpu_gpu_mixed_init(devices=1)      # GPU 1
ov.settings.cpu_gpu_mixed_init(devices="1")
ov.settings.cpu_gpu_mixed_init(devices="cuda:1")
ov.settings.cpu_gpu_mixed_init(devices=[1])
ov.settings.cpu_gpu_mixed_init()               # unchanged: auto (current device)
```

### Use case (from the issue)

> User A is on GPU 0, User B wants GPU 1, both still want CPU/GPU mixed mode. Explicit device selection avoids resource conflicts.

## How it works

- The spec is parsed into a **single CUDA index** (accepts `int` / `"1"` / `"cuda:1"` / single-element list).
- The index is validated against `torch.cuda.device_count()` — an out-of-range or unparseable value raises a clear `ValueError`.
- It is pinned via `torch.cuda.set_device(idx)`. Because omicverse's mixed-mode kernels resolve a bare `"cuda"` through `torch.cuda.current_device()` (`normalize_torch_device`), they now land on the selected GPU with no other changes.
- The choice is recorded in `ov.settings.device` (e.g. `"cuda:1"`); `devices=None` keeps it `None` and preserves the historical auto behaviour.
- Also drops a hard-coded `"cuda:0"` in the sccomposite RNA fit so it honours the pinned device via `current_device()`.

## Tests

`tests/utils/test_settings_mixed_devices.py` — parsing/pinning across the accepted spec forms, `None` auto path, out-of-range `ValueError`, unparseable `ValueError`. **3 passed** locally on an H100 (single-GPU node; the multi-GPU routing relies on the standard `torch.cuda.set_device` → `current_device` contract).

Thanks to @Yippee3 for the request.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e954f986dd06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** ov.pp.leiden: resolution lists in every mode (cpu / mixed / gpu)

## Description

#1022 made `ov.pp.leiden` accept a list of resolutions only in `cpu` mode; in `cpu-gpu-mixed` and `gpu` mode a list still raised, so the same call behaved differently per mode.

- A list of resolutions now works in every mode. Labels go to `obs[f"{key_added}_{r}"]`, and the first resolution also to `obs[key_added]`.
- `backend='cpp'` clusters the resolutions in parallel on the CPU. The GPU modes run one resolution after another.
- A length-1 list is still treated as a scalar (#877).
- New test `test_pp_leiden_resolution_list_same_keys_in_every_mode` covers `cpu` and `cpu-gpu-mixed`; the mixed case is skipped without torch.
- `test_leiden_identical_on_same_graph` now requires leidenalg >= 0.12, the version the exact C++ port reproduces. With leidenalg 0.10.2, 4/1482 labels differ.

Tests:
- Env with torch and leidenalg 0.10.2: `tests/pp/test_leiden_resolution.py` + `tests/pp/test_cpp_backend.py`: 9 passed, 1 skipped.
- Env without torch: the 3 existing GPU-Leiden tests fail on `import torch`, as on master; the rest pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7366434cfbc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
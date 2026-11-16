# Issue

**Title:** Expose `random_state` in `tl.draw_graph`

## Description

Exposes the `random_state` parameter of `cugraph.layout.force_atlas2` in `tl.draw_graph` (previously hard-coded to 0). The random state is also passed to `get_init_pos_from_paga` when `init_pos='paga'`, thus better matching Scanpy behaviour.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55b331f75214`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
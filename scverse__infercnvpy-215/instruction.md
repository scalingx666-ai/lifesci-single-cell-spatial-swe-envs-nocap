# Issue

**Title:** fix(pl): leave out heatmap labels that would overlap

## Description

Summary: In the fast chromosome heatmaps, labels of very small groups and of narrow chromosomes overlapped, as they did with the previous scanpy-based renderer. This PR leaves out labels that would overlap a label already drawn, so the remaining labels stay readable. Labels of groups with enough room are drawn exactly as before.

Changes:
- On every draw, each group and chromosome label is measured at its real font and rotation, with a small gap. Labels are kept largest group (or widest chromosome) first; a label is left out only if it would overlap one already kept.
  - Because this runs on every draw, it holds at any figure size and dpi, also with `bbox_inches="tight"`.
  - It applies to both orientations (`swap_axes`) and to `pl.chromosome_heatmap_summary`.
- Group labels are thinned through a tick formatter, so tick positions and the axis label stay where they were.
- Legacy mode is unchanged.

Testing:
- A new test with tiny groups and narrow chromosomes checks, for both plots and both orientations, that the drawn labels' bounding boxes never intersect and that large groups keep their labels. It fails on main.
- A second test checks that every label is drawn when groups are of normal size.
- Group labels in normal-sized figures are pixel-identical to main. The image baselines changed only where chr21 and chr22 overlapped.
- The full suite passes on the HMGU cluster (489 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c488d5934f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
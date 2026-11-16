# Issue

**Title:** Fix prior finding bug and add input arguments to force priors

## Description

But also revamps and improves the heuristic prior-finding even more.

Adds the following command-line input arguments:
```console
  --force-cell-umi-prior FORCE_CELL_UMI_PRIOR
                        Ignore CellBender's heuristic prior estimation, and
                        use this prior for UMI counts in cells. (default:
                        None)
  --force-empty-umi-prior FORCE_EMPTY_UMI_PRIOR
                        Ignore CellBender's heuristic prior estimation, and
                        use this prior for UMI counts in empty droplets.
                        (default: None)
```

which will hopefully allow users to handle tricky cases where they just want to override CellBender's heuristics and manually specify the priors themselves.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d83e7e75c567`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
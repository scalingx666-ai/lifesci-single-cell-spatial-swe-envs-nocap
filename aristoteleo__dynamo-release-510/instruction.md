# Issue

**Title:** Do NOT replace layers spliced/unspliced with pearson residual normalized data

## Description

#### what does "skipping set X as layer in adata.layers" mean? 
-> Need to check because the current implementation is like below..
```
        if layer == DKM.X_LAYER:
            # TODO: discuss if we need X set in layers
            # X layer will only be used for X_pca
            main_info("skipping set X as layer in adata.layers", indent_level=2)
            continue
```

#### did you replace layers spliced/unspliced with pearson residual normalized data? 
-> This probably a bug... so code is updated to do not replace layers spliced/unsplice.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4c704663079`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
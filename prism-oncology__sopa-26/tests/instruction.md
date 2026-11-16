# Issue

**Title:** Adding patch embeddings

## Description

Related to #19 

I added a patch embedding functionality for WSIs. Specifically, patches are retrieved with a specific `patch_width` from a specific `magnification` level. Then they are pushed as batches of `batch_size` into one of three embedding models. The resulting embeddings are stored as an additional image within the spatialdata object with index the class of the embedding model. 

in order to test it you can run the following:

```python
import spatialdata_plot
from sopa.io import wsi
from sopa.segmentation.tissue import hsv_otsu
from sopa.embedding.patches import embed_wsi_patches

slide = wsi('https://openslide.cs.cmu.edu/download/openslide-testdata/Aperio/CMU-1.svs')
hsv_otsu(slide, "CMU-1")
embed_wsi_patches(slide, "CMU-1", "Resnet50Features", 10, 224, 64, num_workers=8)

slide.pl.render_images("Resnet50Features", channel=[1, 2, 3]).pl.show()
```

the output of the plotting function using only the first 3 channels of ResNet features looks like this:

![2024-02-13 17 06 31](https://github.com/gustaveroussy/sopa/assets/4221880/c04848f1-cfaf-4f53-9a0b-625073df0223)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ecba5f9fef6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
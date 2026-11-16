# Issue

**Title:** Added more complex tissue detection method for complexer tissues

## Description

Segmenting this image is hard:

<img width="611" height="479" alt="image" src="https://github.com/user-attachments/assets/3b03b7ef-a634-4c5c-acb7-1290b2c9e6e3" />

Otsu f.e. yields
<img width="611" height="479" alt="image" src="https://github.com/user-attachments/assets/0bc57330-9d43-4065-9bc1-a7ea583d01cc" />
since we have very dark regions in the image with background-esque areas inbetween.

The new method, inspired by [this](https://scikit-image.org/docs/0.25.x/auto_examples/segmentation/plot_trainable_segmentation.html) is based on the assumption that the corners are background, then uses randomforest to classify the tissue into bg and fg and finally refines the mask.

```
sq.experimental.im.detect_tissue(
    sdata,
    image_key="hne",
    method="weka",
    n_samples=2,
)
```
<img width="611" height="479" alt="image" src="https://github.com/user-attachments/assets/83b0801b-ad9f-44fd-bb39-56d7ef8e65a6" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91dd574969a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
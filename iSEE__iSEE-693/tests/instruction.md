# Issue

**Title:** Added tabTitle argument for iSEE

## Description

Hi!

As discussed in the , the tab title for miaDash is currently derived from the `dashboardHeader` title and therefore is not rendered correctly when the title is an HTML element, like for miaDash.

![Screenshot 2025-04-01 at 23 05 09](https://github.com/user-attachments/assets/6bc5d805-ff0c-445d-ad24-2117922aad4d)


Therefore, I added a new argument to the `iSEE` function called `tabTitle`, which lets you modify the name of the browser tab without affecting the app title or other elements. For example, for the ISEE app:

![Screenshot 2025-04-01 at 23 02 38](https://github.com/user-attachments/assets/84412b4e-2bfe-4810-bd52-315f4810fe01)

Feel free to let me know if this solution suits iSEE and if anything should be changed.

Best,
Giulio

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55c1d1815d5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
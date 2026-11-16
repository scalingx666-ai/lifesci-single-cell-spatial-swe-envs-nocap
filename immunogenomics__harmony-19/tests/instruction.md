# Issue

**Title:** New vignette and website

## Description

Hi Ilya,

I created a new vignette (getting_started.Rmd) that applies Harmony to integrate two PBMC datasets without using Seurat objects. The vignette also highlights why Harmony should be used to identify common cell-types and how not using Harmony may result in identifying batch-driven clusters. 

There is also a new /docs folder which has a copy of the main README.md and compiled getting_started.md that can be used as a website. You will need to go into your settings > GitHub Pages > master branch /docs folder to make the website accessible at http://immunogenomics.github.io/harmony
Additional css styling/themes can be added to the website in case you're interested: https://jekyllthemes.io/free

Feel free to edit and let me know if you have any questions. 

Best,
Jean

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f071627f4ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
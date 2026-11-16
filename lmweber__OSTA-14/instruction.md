# Issue

**Title:** Update image segmentation and Loupe chapters

## Description

This also involved:

* Adding a few imagese
* Re-organizing some material in the Space Ranger chapter
* Adding citations

I also:

* Re-organized citations in alphabetical order
* Added DOI and URL for all citations
* Added an icon (you can change the png files later)
* Updated the contributors and listed all package used as a thank you
* Updated the intro to ST
* Added links to materials from my team to help others get started with R/BioC

In addition, you might want to add an html file like
https://github.com/lcolladotor/bioc_team_ds/blob/master/map_and_ga.html
using https://github.com/lcolladotor/bioc_team_ds/blob/master/index.Rmd#L12-L13
such that you can include a map of your visitors, keep track of visitor
stats using Google Analytics, add a license icon, etc. See the end of
https://lcolladotor.github.io/bioc_team_ds/authorship.html#.YQy6DtNKgdk for
an example.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78482aa9a2bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Fixed marker reporting for the custom selections.

## Description

`CustomSelectionsState#fetchResults(<selection_name>)` will return a `ScoreMarkersResults` object, but inside that object, the selection is encoded as group 1 (as mentioned [here](https://www.kanaverse.org/bakana/CustomSelectionsState.html#fetchResults)); you can't pass a name string in there, as Embind will probably just guess and convert it to zero. 

Same for the standalone, but I haven't checked out where that is.

Imagine that this is kind of like how we have to decrement in `MarkerDetectionState#fetchResults`. 

, probably.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d452e66d7e7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
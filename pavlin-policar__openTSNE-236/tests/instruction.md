# Issue

**Title:** Fix exploding memory problem in BH for duplicate rows

## Description

##### Issue
For data sets with duplicate rows, e.g. titanic, the BH approximation would error out with memory errors as the points in the embedding would be forced too close, and thus the BH splitting would go on seemingly without end.

This was brought about with a recent change where we fixed the collapsing embedding problem. The fix there was to allow BH to make more splits in the space, thus enabling the embeddings to properly expand after the EE phase.

##### Description of changes

My working fix reverts the old limit to node splitting at 1e-6. However, I leave the duplicate detection limit at machine precision, otherwise we'd run into the same EE collapse issue as before.

This now means that points that are too close together will get grouped into the same BH box. This, however, introduces a new problem. This means that BH won't be able to detect self-interactions for leaf boxes which contain more than one data point. This means that any such points will consider self-interactions, which technically isn't correct.

However, I believe this is not an issue as standard embeddings span a larger space, and this should rarely occur. In the case that it does occur, it should occur in the EE phase. And if it occurs there, that should be fine, as the points will drift apart in the standard phase, and each point will be assigned to its own BH box. This means that even though some points may be incorrectly computing their negative gradients in the EE phase, this should be rare and small, and should only nudge them a bit further apart. And anyhow, this is all fixed in the standard phase of the embedding.

There is one other case where this can occur, if the user decides to run the entire embedding with a higher than normal exaggeration. Again, this should only cause points to be pushed out marginally more than normally and there really isn't any perceivable difference in the embeddings.

Therefore, even though this introduces some small errors in the negative gradient computation in very rare cases, it completely gets rid of memory errors, which are a much larger problem IMO.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99e97d9673ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
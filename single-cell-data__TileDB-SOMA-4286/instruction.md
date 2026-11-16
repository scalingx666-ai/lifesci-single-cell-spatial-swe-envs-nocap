# Issue

**Title:** [python, C++] fix group handling issues

## Description

Core team pointed out there is a performance deficiency in our calls to Group `add` -- we should be specifying the type of the object being added.  While this parameter is optional, not specifying it will incur a performance penalty.

While implementing this, I also noticed a bug in the `Collection.members` and `SOMAGroup._set_element` -- every member added to a Collection would be reported as soma_type==Collection by the `members` method. This was due to a typo in the group add call.

Summary of changes:
* TileDB object type now passed to Core Group.add
* `Collection.members` unit test now checks for the actual object type, rather than hard-coding "Collection"
* Fix SOMAGroup to correctly set collection member type.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99a2c140f37b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
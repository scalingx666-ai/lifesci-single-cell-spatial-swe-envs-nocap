# Issue

**Title:** Fix annotation

## Description

This PR solves the issues mentioned in #260.  The save message has been corrected and there are also no duplicate table names.
Regarding the latter point of adding new entries, saving and then going back to the old table leading to issues with non matching indices, I opted to delete the previous table. The other option would be to do a left exclusive join to see if there are indices not present in the table and then specifically add a row, but this seemed a bit more cumbersome. However this can be discussed.

We have a couple of cases for saving / exporting for element and table that are already stored:
1 shape name stays the same but table name is changed: in this case we can assume that new elements have been added making the old table invalid for the shape element. Thus the table with the old name is removed.
2 shape name is changed, but table name stays the same: this could be dealt with by a join but it is save to assume the user meant to delete the old shape element.
3 Both names are changed: this can be if there are diverging paths, no elements are deleted, new elements are just added.

Furthermore, if the spatialdata object is not backed, the elements are only added in memory and a notification is given that the spatialdata object is not backed and the elements are only added in memory.

Lastly, the first row with the default undefined class is now set not to be editable. The reason for this is that if someone has a shapes layer annotated with the default class, but then reopens it while having changed the default class, this results in an error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2d02dd2bc8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Update napari to 0.6.2, add bermuda, new shortcut for linking layers, deprecated access to _dock_widgets

## Description

With this PR the plugin uses only napari 0.6.2 and up. Also, bermuda can optionally be installed. Next, the command for linking layers has been changed to 'Ctrl-L' (command key on MacOS). This, because 'Shift-L' is now used to switch to poly line drawing in the 'Shapes' layer.
Lastly, the deprecated access of "_dock_widgets" has been changed to accessing the public property in order to silence the warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aea2eb559c53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
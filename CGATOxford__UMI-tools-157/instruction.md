# Issue

**Title:** added import at start of umi_tools

## Description

umi_tools crashes when running on a system without a graphical interface.

```  File "python3.6/tkinter/__init__.py", line 2017, in __init__
    self.tk = _tkinter.create(screenName, baseName, className, interactive, wantobjects, useTk, sync, use)
_tkinter.TclError: no display name and no $DISPLAY environment variable
```

small fix that worked on my cluster

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2741904127f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
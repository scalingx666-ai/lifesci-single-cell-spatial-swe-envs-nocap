# Issue

**Title:** Travis CI: flake8 finds syntax errors and undefined names

## Description

Add [flake8](http://flake8.pycqa.org) tests to find Python syntax errors and undefined names.

__E901,E999,F821,F822,F823__ are the "_showstopper_" flake8 issues that can halt the runtime with a SyntaxError, NameError, etc. Most other flake8 issues are merely "style violations" -- useful for readability but they do not effect runtime safety.
* F821: undefined name `name`
* F822: undefined name `name` in `__all__`
* F823: local variable name referenced before assignment
* E901: SyntaxError or IndentationError
* E999: SyntaxError -- failed to compile a file into an Abstract Syntax Tree

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0df498b18f41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
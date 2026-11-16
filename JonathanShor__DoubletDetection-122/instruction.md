# Issue

**Title:** Create coding standards

## Description

I believe we should conform to a coding style. 

- Proposed use of the black formatter and flake8 linter (using the settings from black)

- Added pre-commit hooks (via pre-commit package) so that we do not commit non-compliant code

- Added .editorconfig file, which vscode will use to override settings for this project

https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig

- Added CONTRIBUTING.rst for explanation of how to contribute

VS Code will also recognize the setup.cfg file to override default flake8 args.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13710e845ee2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
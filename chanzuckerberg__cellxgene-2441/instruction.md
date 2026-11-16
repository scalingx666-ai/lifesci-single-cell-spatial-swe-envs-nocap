# Issue

**Title:** feat: removing sastisfaction gh action for gh app

## Description

This PR removes the sastisfaction github action. 

## Notes

* We have refactored sastisfaction to be a  github app and is already running on this repo
* The app does the exact same thing as the action, but runs much faster (seconds instead of minutes) and easier to configure
* The app has repo-specific configuration coming soon, so you will be able to add, edit, and create your own rules
* If you notice the app blocking a build or throwing unknown errors, please reach out to @jacobrheath @jakelerner-czi @edulop91

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0263f6ce59d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
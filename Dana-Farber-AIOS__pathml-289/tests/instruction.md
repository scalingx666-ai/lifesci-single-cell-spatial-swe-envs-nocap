# Issue

**Title:** dont use default pip version

## Description

Our testing suite has been hanging during environment setup, at the step of installing pip dependencies (for example: https://github.com/Dana-Farber-AIOS/pathml/runs/5043141558?check_suite_focus=true#step:6:1065)

Not sure why this started happening, since all the versions are pinned and we didn't change anything. May be connected to a change in pip itself; the last working test used pip version 21.3.1 ([log here](https://github.com/Dana-Farber-AIOS/pathml/runs/4987117042?check_suite_focus=true#step:6:347)) but the more recent tests have been using recently released pip version 22 ([log here](https://github.com/Dana-Farber-AIOS/pathml/runs/5008770944?check_suite_focus=true#step:6:347))

This tries to fix by adding `add_pip_as_python_dependency: false` to config, so that pip is installed from the environment file instead of by default (this should mean that it will respect the pinned pip version, which I don't think it's doing now). Also pins pip to a version that we know is able to resolve the environment successfully.

Similar to #288 but I think this would be more maintainable, since it doesn't actually make any changes to the requirements themselves

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2eca9ed02e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
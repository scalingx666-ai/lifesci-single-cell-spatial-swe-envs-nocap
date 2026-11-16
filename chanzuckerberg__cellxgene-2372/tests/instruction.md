# Issue

**Title:** fix: thuang-fix-tsconfig-path

## Description

Bruce was having issue with VS Code thinking the `tsconfig.json` file is one level up from the `client` folder, so explicitly setting the project path relative to `eslint.js` lives seems more reliable and works for both me and Bruce

@MillenniumFalconMechanic or @seve please help test your VS Code to see if you still get eslint's type hints 🙏 

Thanks so much!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26de334274da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
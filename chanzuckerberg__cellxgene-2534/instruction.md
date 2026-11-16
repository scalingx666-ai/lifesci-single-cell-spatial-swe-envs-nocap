# Issue

**Title:** chore(webpack): remove script-ext-html-webpack-plugin

## Description

#### Reviewers
**Functional:**  @roaga 

---

## Changes
- remove
   - Removes [script-ext-html-webpack-plugin](https://github.com/numical/script-ext-html-webpack-plugin), this repo is 
   - Good news is that as of [v5.0.0](https://github.com/https://github.com/jantimon/html-webpack-plugin//blob/main/CHANGELOG.md#500-2021-02-03), [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin/) defaults scripts to type=defer

cc: @tihuan, might want to take a look at this when you get back 😸

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b4c1e418e1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
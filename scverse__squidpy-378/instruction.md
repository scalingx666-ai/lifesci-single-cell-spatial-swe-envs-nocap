# Issue

**Title:** add classes overview for each class

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [x] New feature (non-breaking change which adds functionality)

### Description

Change how classes are displayed in the docs. Add an overview table for each class. Resulting docs:
![Pasted Graphic](https://user-images.githubusercontent.com/13350159/124102134-615afa80-da60-11eb-9c96-14c794224b78.png)
![Pasted Graphic 1](https://user-images.githubusercontent.com/13350159/124102193-6e77e980-da60-11eb-8fa5-cd4de306491a.png)

￼
Remaining issue (not sure how to solve): Long names in the sidebar. I tried to remove the prefix by adding `add_module_names=False` in the config, but that did not seem to have an effect.
￼![Pasted Graphic 2](https://user-images.githubusercontent.com/13350159/124102121-5e600a00-da60-11eb-9cd2-55cdf7b5598b.png)



### How has this been tested?
<!--- Describe how you've tested your changes: -->
...

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->
...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a31729690f04`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
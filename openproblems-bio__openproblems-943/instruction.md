# Issue

**Title:** Read the task commit from task_info.yaml

## Description

## Describe your changes

`get_task_info` hardcoded the commit, so every `task_info.json` we have ever
published carries `"commit": null`:

```r
commit = jsonlite::unbox(NA_character_), # TODO: Add when available in task_info.yaml
```

It now reads the field:

```r
commit = jsonlite::unbox(task_info_yaml$commit %||% NA_character_),
```

The `%||%` is there for the null rather than as a placeholder -- `unbox(NULL)`
serialises to `{}`, not `null`, so dropping it entirely would change the shape of
the output for every task that does not write the field yet:

```r
jsonlite::toJSON(list(commit = jsonlite::unbox(list()$commit)))
#> {"commit":{}}
jsonlite::toJSON(list(commit = jsonlite::unbox(list()$commit %||% NA_character_)))
#> {"commit":null}
```

## Issue ticket number and link


## Checklist before requesting a review
- [x] I have performed a self-review of my code

- Check the correct box. Does this PR contain:
  - [ ] Breaking changes
  - [ ] New functionality
  - [ ] Major changes
  - [ ] Minor changes
  - [x] Bug fixes
  - [ ] Documentation

- [x] Proposed changes are described in the CHANGELOG.md

- [ ] CI Tests succeed and look good!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fe740d9899e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
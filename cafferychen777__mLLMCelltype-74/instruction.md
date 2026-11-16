# Issue

**Title:** refactor(r): use standalone template for reasoning annotation prompt

## Description

Address PR review feedback: create_reasoning_annotation_prompt() no longer derives its prompt from create_annotation_prompt() via regex substitution, removing the fragile coupling to the base prompt's trailing instruction. Input normalization is mirrored in an internal prepare_annotation_prompt_data() helper so the reasoning prompt keeps the same canonical cluster ordering without depending on the base prompt's text; create_annotation_prompt() itself is unchanged from upstream.

The reasoning prompt now mirrors Python's REASONING_PROMPT_TEMPLATE so both implementations request the same structured JSON output, adapted to the R signature's single tissue_name argument.

## Description

**What does this PR do?**
<!-- Brief summary of the changes -->

**Why is this change needed?**
<!-- Explain the problem this solves or the value it adds -->

### Related Issues
<!-- Link any related issues -->
- Fixes #
- Related to #

## Type of Change

- [ ] Bug fix (non-breaking change that fixes an issue)
- [ ] New feature (non-breaking change that adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Test improvements
- [ ] Refactoring (no functional changes)
- [ ] Performance improvement

## Testing

<!-- Describe the testing you've done -->
- [ ] All existing tests pass
- [ ] New tests added for changes
- [ ] Tested with real data (if applicable)

**Test Environment:**
- R/Python Version:
- Operating System:

## Checklist

- [ ] Code follows the project's coding standards
- [ ] Self-review of the code completed
- [ ] Documentation updated if needed
- [ ] No API keys or sensitive data exposed
- [ ] I have read and agree to the [Contributing Guidelines](CONTRIBUTING.md)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `322f41e3ed8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
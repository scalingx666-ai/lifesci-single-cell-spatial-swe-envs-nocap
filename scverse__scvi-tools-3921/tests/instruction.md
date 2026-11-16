# Issue

**Title:** docs: render de_silent docstring placeholder in model methods

## Description

### Problem

Several public model methods use the `%(de_silent)s` docstring template
placeholder (defined in `scvi/utils/_docstrings.py` and registered in the
`de_dsp` processor) but are **not** decorated with `@de_dsp.dedent`. As a
result the placeholder is never substituted, and the literal string
`%(de_silent)s` is rendered in the docstrings and the online API reference
instead of the `silent` parameter description.

Reproducer:

```python
import scvi
print(scvi.model.SCVI.get_normalized_expression.__doc__)
# ...
#         return_numpy
#             ...
#         %(de_silent)s        <-- literal placeholder shown to users
#         dataloader
#             ...
```

### Fix

Apply the existing `@de_dsp.dedent` decorator (already used on the
`differential_expression` methods in the same files) to the affected methods:

| Model | Methods |
|-------|---------|
| `RNASeqMixin` (SCVI, LinearSCVI, …) | `get_normalized_expression`, `get_feature_correlation_matrix` |
| `TOTALVI` | `get_normalized_expression`, `get_protein_foreground_probability`, `get_feature_correlation_matrix` |
| `MULTIVI` | `get_normalized_expression`, `get_protein_foreground_probability` |
| `ContrastiveVI` | `get_normalized_expression` |
| `MRVI` | `get_normalized_expression` |
| `RESOLVI` | `get_normalized_expression`, `get_normalized_expression_importance` |

The change is documentation-only in effect: it adds the decorator (and the
`de_dsp` import where missing) so the placeholder is substituted. No runtime
behavior changes.

### Tests

Adds `tests/model/test_docstrings.py`, which parametrizes over the public
model classes and asserts that no public method exposes an unsubstituted
`%(...)s` placeholder. The test fails before this change (11 methods) and
passes after.

### Note / follow-up

`scvi.external.METHYLVI.differential_methylation` has the same missing-decorator
issue, but additionally references placeholders that are **not** defined in any
processor (`%(de_mdata)s`, `%(de_modality)s` — the latter with no matching
parameter in the signature). That case needs new placeholder definitions and a
small signature/docstring reconciliation, so I left it out of this PR to keep
the change focused. Happy to address it in a follow-up if desired.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `455f610c6dc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
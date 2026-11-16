# Issue

**Title:** Fix: scArches query mapping for models using a batch embedding

## Description

# Summary
In scArches query-to-reference mapping (load_query_data), when the reference model was trained with batch_representation="embedding", the query latent never moved during surgery. One-hot batches were unaffected.

# New Tests

- test_scvi_query_to_reference_mapping: makes sure reference latent stays intact (<1e-4) while the query latent updates (>1e-3); the embedding case asserts the batch embedding grew and is trainable.

- test_scvi_query_to_reference_freezes_reference_embedding_rows: For models with batch embedding, this ensures the reference embedding rows (weights) remain frozen (<1e-8) and only the new query row updates (>1e-3). This test can be removed as it relies on too many implementation details.

# Fix
This fixes it with a one-line change to the online-update freezing logic.

# Details (Root Cause)
During surgery, _set_params_online_update freezes the whole network except a small allow-list of parameters (requires_grad=True only for first-layer FC weights, batchnorm under certain options, etc.). The batch embedding parameter (_embeddings_dict.batch.weight) wasn't on that allow-list, so it was frozen entirely — including the newly added row for the query batch. With that row frozen, the query batch had no learnable representation and the query latent stayed fixed.

# Important note
If a query dataset also contains reference batch categories, those reference embedding rows would receive a gradient. This can also be fixed with a few more lines of code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b499dc22dd1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
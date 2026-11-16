# Issue

**Title:** fix(space): validate COMMOT and FlowSig inference and summaries

## Description

## Correctness and user-visible behavior

COMMOT CPU aggregation previously ignored requested scaling: six unit-weight edges returned a mean of 1 even with scale_factor='sum'. FlowSig matched ligand prefixes, so WNT1 received WNT10's signal, turning [1,2] into [11,22]. This change fixes both numerical defects and builds an AnnData-first path from COMMOT inference to FlowSig network learning.

The final diff changes communication code, tests and opt-in runtime extras. No CI workflow or setup.py change is included. Existing repository workflows remain unchanged. The commot/flowsig extras describe actual optional runtime dependencies; default dependencies are unchanged.

## Public APIs

- `ov.space.run_commot(...)` takes explicit database, expression layer, coordinates, cutoff and units. It preserves native commot-* results and records provenance. Coordinates are the distance source, so stale cached distances are not reused. Existing namespaces require explicit overwrite. Backend failure leaves input unchanged. A distance-matrix allocation check prevents an unannounced quadratic allocation.
- `ov.space.create_communication_anndata(..., database_name=..., level='lr', statistic='sum')` uses database identities rather than parsing hyphenated names. Legacy level='all' warns about overlapping levels. Missing database metadata or ambiguous selection fails with an actionable error. Plot-compatible layers retain their names while actual score and p-value semantics are recorded.
- `ov.space.run_flowsig(...)` consumes supplied GEMs and COMMOT marginals, uses explicit spatial blocks, and retains raw, biologically validated and filtered adjacency matrices. It does not substitute GEM algorithms or perform implicit Moran filtering. It records the backend bootstrap-index seed policy. Multiple independent libraries must be analyzed separately; joint multi-sample inference is not advertised.

## Migration and limits

- Previously unscaled CPU outputs now honor sum/numeric/auto, including the legacy default auto. Reconstruct FlowSig inputs and downstream networks affected by ligand prefix collisions.
- Summary metadata now distinguishes unknown annotations and score meaning. level='all' is compatibility-only; use one level before aggregating columns.
- COMMOT scores are model transport scores. Summary p-values test cell-type labels on a fixed graph; FlowSig edge weights are bootstrap frequencies. Neither supplies condition-level replicate inference or experimental proof of causality.
- The runners intentionally support independent single-library analyses with supplied GEMs. Dense-distance memory checks cover the distance matrix only, not total solver memory.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
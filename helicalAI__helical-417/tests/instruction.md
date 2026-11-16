# Issue

**Title:** fix(genept): make the Ensembl to gene-symbol mapping reachable

## Description

Fixes helicalAI/bio-agent#1121. Companion to helicalAI/bio-agent#1127; diagnosis in helicalAI/bio-agent#1117.

## GenePT's Ensembl → symbol mapping was dead code

GenePT's embedding table is keyed on gene **symbols** (`get_text_embeddings` looks up `self.embeddings.get(emb.upper())` over `var_names`), so Ensembl IDs must be mapped *to* symbols — the opposite direction from the Ensembl-keyed models. The guard read:

```python
if gene_names == "ensembl_id":          # '==', not '!='
    if adata.var[gene_names].str.startswith("ENS").all() or ...:
        raise ValueError("... Please set gene_names='ensembl_id' ...")
    adata = map_ensembl_ids_to_gene_symbols(adata, gene_names)
```

copied from Geneformer, where the correct comparison is `!=`. The mapping was therefore unreachable on every input where it would have been correct:

- `gene_names="ensembl_id"` with real Ensembl IDs **raised**, telling the caller to set the flag they had just set;
- `gene_names="ensembl_id"` with non-`ENS` values mapped "Ensembl → symbols" over data that was not Ensembl;
- `gene_names="index"` — the default, and the only value bio-agent can reach, since `FineTuning.predict` calls `process_data(data)` positionally — skipped mapping entirely and looked Ensembl IDs up in a symbol-keyed table.

The docstring was also copied from Geneformer and described the opposite model ("GenePT uses Ensembl IDs to identify genes"). Rewritten to match reality.

## Detection

Per entry against an anchored Ensembl *gene* ID pattern, rather than `.startswith("ENS").all()`. The latter also matches real gene symbols (`ENSA`) and transcript/protein IDs (`ENST…`, `ENSP…`), and `.all()` skips a var index that is only mostly Ensembl IDs. Entries already symbols are preserved, so a mixed index does not lose them.

## Two further defects, caught by committee review and fixed in the second commit

Both were introduced by making the guard reachable — before that, the default path never ran the mapping, so neither was reachable for exactly the inputs this fix exists to serve.

1. **Version-suffixed IDs were silently dropped.** The pattern accepts `(\.\d+)?`, but the matched identifiers went to the mapping table unstripped, and that table is keyed on bare `ENSG…`. Verified: TP53 and ACTB vanished from `[ENSG00000141510.17, ENSG00000075624.9, ENSG00000111640]`, leaving only unversioned GAPDH. Versioned IDs are the GENCODE/CellRanger default. Stripped now, and only for entries matching the Ensembl pattern — real symbols contain dots too (`AC000068.10`).

2. **Duplicate symbols crashed `process_data`.** Ensembl → symbol is many-to-one: 10,616 of the 48,698 symbol-bearing rows in `hsapiens_pybiomart.csv` share a `gene_name` (3,369 symbols carried by ≥2 IDs). A non-unique `var_names` made this function's own `adata[:, genes_names]` raise `InvalidIndexError: Reindexing only valid with uniquely valued Index objects`. Verified with `ENSG00000274144` + `ENSG00000105618` (both → `PRPF31`). Collapsed now to the copy carrying the most counts, so an all-zero alt-scaffold copy cannot displace the expressed one.

Also drops the `adata.copy()`: the helper only reads one `var` column, so `convert_list_ensembl_ids_to_gene_symbols` is called directly — measured 13.9 MB vs 62.1 MB peak on a 4000×3000 float32 AnnData — which additionally removes the coupling to the helper's hardcoded `"gene_names"` output column.

## Tests

`ci/tests/test_genept/` **did not exist** — that is why the inverted guard survived. 11 tests added, covering both identifier systems, mixed indexes, `ENSA`, versioned IDs, symbol-less IDs, collisions, expressed-copy selection, and a non-index `gene_names` column.

Two of them initially passed for the wrong reason and were fixed only after confirming the mutation passed against them: `test_version_suffixed_ids_are_mapped` asserted only that no `ENSG` prefixes remained (which dropping satisfies as well as mapping), and `test_gene_names_column_is_honoured` asserted nothing at all, since the fixture's index holds no `ENSG` values either way.

Mutation-tested: restoring the unreachable guard, remapping wholesale instead of per entry, removing the version strip, positional dedupe, and gating the mapping on `gene_names == "index"` each turn the suite red.

`pytest ci/tests/test_genept ci/tests/test_utils` → 33 passed, 1 skipped. `black` clean. Version bumped 3.0.3 → 3.0.4 (PATCH: bug fix).

## Note on scope

The other four models still use the inlined `.startswith("ENS").all()` check, with the `ENSA`/`ENST` and all-or-nothing weaknesses described above. Unifying them on one detector is tracked separately in helicalAI/bio-agent#1123 — it is a behaviour change across Geneformer, Tahoe, Nicheformer and Transcriptformer, and keeping it out means this correctness fix is not blocked behind it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9f9fe788311`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
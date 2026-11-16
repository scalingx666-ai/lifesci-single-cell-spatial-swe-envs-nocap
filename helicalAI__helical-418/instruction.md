# Issue

**Title:** feat: handle Ensembl/symbol gene identifiers in each model's process_data

## Description

Reconciles gene identifiers inside each model's `process_data`, so an AnnData indexed by Ensembl gene IDs works with the symbol-keyed models and vice versa. **Stacked on #417** (GenePT's inverted guard), which is now merged.

## Approach

`process_data` is the single choke point shared by `embed`, `fit`, `evaluate`, `eval/` and `run_isp`, so handling identifiers there covers all five at once. Per-model knowledge also stays in per-model code, rather than in a table that has to be kept in step by hand.

## One shared set of primitives, five inlined copies removed

`startswith("ENS")` appeared inline in Geneformer, Tahoe, Nicheformer, GenePT and Transcriptformer's dataloader. It had three live bugs, each now covered by a test:

| Bug | Consequence |
|---|---|
| Matches real gene symbols (`ENSA`) and transcript/protein IDs (`ENST…`, `ENSP…`) | Real genes dropped or misrouted |
| `.all()`/`.any()` can't express a *mostly*-Ensembl index | Conversion skipped entirely, or symbols mapped to NaN |
| Version suffixes never stripped | Every `ENSG….17` — the GENCODE/CellRanger default — resolves to `None` and is dropped |

Replaced by `ENSEMBL_GENE_ID_PATTERN` (anchored), `is_ensembl_gene_id`, `ensembl_id_mask` (per entry), `strip_ensembl_version` (Ensembl-matching values only — real symbols contain dots, `AC000068.10`).

## Per model, by what the vocabulary is keyed on

- **scGPT, UCE, GenePT** (symbols) → `ensure_gene_symbols`. Translates Ensembl IDs, leaves existing symbols alone so a mixed index keeps both, and collapses symbols claimed by more than one gene. That collapse is not optional: 10,616 of the 48,698 symbol-bearing rows in the bundled table share a `gene_name`, and a non-unique var index desyncs scGPT's `count_matrix` from its `gene_ids` (#377) and raises `InvalidIndexError` in GenePT. Of a colliding set the copy carrying the **most counts** wins — choosing positionally lets an all-zero alt-scaffold copy displace the expressed one, after which the gene reads as unexpressed with no error anywhere.
- **Geneformer, Tahoe** (Ensembl) → `ensure_ensembl_ids`. Ensembl input is taken **directly** instead of raising, and deliberately *not* round-tripped through symbols: their vocabularies contain genes with no gene symbol at all, so a round trip drops them. `ENSG00000159239` — in Geneformer's vocabulary, blank symbol in the table — is now tokenized rather than lost. `var_names` are left untouched, so reverse lookups and caller-supplied gene lists keep addressing the caller's own identifiers.
- **Nicheformer, Transcriptformer** — already branched on the identifier system correctly; only the detector changed.

The two helpers are deliberately asymmetric — one writes a column, the other the index — because their consumers are. Both docstrings now state the rule and the evidence.

## Two protections restored explicitly

The guards being removed caught two things *by accident*, and an existing test encoded them. Rather than re-baseline that test, both are now checked directly — so **`test_ensembl_data_is_caught` passes unmodified**:

- `require_vocabulary_overlap` — rejects well-formed identifiers from another annotation (mouse IDs against a human vocabulary). Membership rather than shape, so usable Ensembl input is accepted while unusable input still fails loudly instead of tokenizing to nothing. Neither Geneformer nor Tahoe had a zero-overlap check before.
- `reject_null_identifiers` — refuses literal `"None"`/`"nan"`/empty placeholders, which mean an earlier mapping step already failed. Matched *exactly*, not by prefix, so real genes like `NANOS1` and `NAT1` are unaffected (the old check used `startswith("None")`).

## Verification

Against **real cached weights on CPU**:

| Case | Before | After |
|---|---|---|
| scGPT, Ensembl index (incl. versioned + symbol-less) | `ValueError: No matching genes found` | 3 genes |
| scGPT, plain symbols | 3 genes | 3 genes (untouched, no conversion) |
| scGPT, mixed index | 0 genes | 3 genes |
| scGPT, two IDs colliding on one symbol | `IndexError`/desync risk | 2 genes |
| Geneformer, Ensembl incl. symbol-less in-vocab gene | raised outright | tokenized, gene kept |
| Geneformer, mouse IDs | raised (by accident) | rejected (deliberately) |

42 new tests for the primitives, including mixed indexes at several ratios, `ENSA`, transcript/protein IDs, versioned IDs, and collapse-by-expression parametrised over *which* copy is expressed — positional selection passes one arrangement and fails the other, so a single fixture would prove nothing.

Suite: **250 passed, 7 skipped, 1 failure** (`test_transcriptformer … gene_mode`, `Torch not compiled with CUDA enabled`, identical on the base commit). `test_helix_mrna` and `test_mamba2_mrna` cannot be collected on the dev host (`mamba-ssm` absent); `test_tahoe` needs `flash_attn` and is verified by CI, which caught two Tahoe tests encoding the previous contract — both since updated.

No repo-wide reformatting: the diff is confined to the twelve files changed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `123705a373b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
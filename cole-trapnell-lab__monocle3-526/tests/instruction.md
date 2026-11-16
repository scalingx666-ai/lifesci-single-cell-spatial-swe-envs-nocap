# Issue

**Title:** Add negative binomial mixed models to expr_models

## Description

#usage:
gene_fits <- fit_models(cds_subset, 
                                    model_formula_str = "~FixedEffect + (1|RandomEffect)",
                                    expression_family = "mixed-negbinomial",
                                    clean_model = T)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63a9e52094cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
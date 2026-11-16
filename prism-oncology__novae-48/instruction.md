# Issue

**Title:** LLM-based naming of the spatial domains

## Description

This pull request adds LLM-based domain annotation to Novae.

Use case 1: annotate directly with an API key
```
from novae.utils import annotate_domains

annotate_domains(
    adata,
    api_key=api_key,
    provider="openai",
    model="gpt-4.1",
)
```
One annotation is generated per domain and added to `adata.obs["novae_domains_X_annotation"]`.

Use case 2: no API key (manual LLM workflow)
```
from novae.utils import annotate_domains, add_domain_annotation

payload = annotate_domains(
    adata,
    return_prompt=True,
)
```
With `return_prompt=True`, Novae does not call any API. It returns the full request payload (messages and output_schema), which can be copied into any LLM manually.

The LLM should return a structured annotation payload matching the schema. You can then pass that output directly to add_domain_annotation:

```
annotation = {
    "annotation": [
        {"novae_domains": "D1011", "annotation": "tumor epithelium", "score": 0.89}
    ]
}

add_domain_annotation(
    adata,
    annotation=annotation,
)
```
This adds one annotation per domain to `adata.obs["novae_domains_X_annotation"]`.

Detailed documentation will be added in a follow-up PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17a681261f88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
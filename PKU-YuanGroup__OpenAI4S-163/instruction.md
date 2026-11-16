# Issue

**Title:** docs(citation): restore the arXiv citation and add CITATION.cff

## Description

## Summary

This PR restores the paper citation for v0.3.0 and makes it available to GitHub's **Cite this repository** button.

- **README:** the **Citing** section returns to both `README.md` and `README_zh.md`, in the same place it was before #161 removed it (bd806681). It carries the arXiv BibTeX for *OpenAI4S: Code as Action, Science as Sessions* (arXiv:2609.15096, cs.AI). The entry matches arXiv's `/bibtex/2609.15096` export, except that the trailing spaces the export leaves on two lines are removed.
- **`CITATION.cff` (new):**
  - `preferred-citation` is the same paper, with the arXiv DOI `10.48550/arXiv.2609.15096`. `doi.org` redirects it to the abstract page.
  - The top level describes the software: MIT license, abstract, keywords, repository URL.
  - `repository-code` appears only at the top level. ruby-cff (the library GitHub Docs names) prefers it over `url` for the BibTeX link, so inside `preferred-citation` it would replace the arXiv link.
  - There is no `version` or `date-released`, so the file is not one more release pin.
- **`tests/test_citation_metadata.py` (new):** checks that the three copies agree, and that the software metadata matches `pyproject.toml`. The rows in `tests/README.md` and `tests/README_zh.md` describe it.

## Area

- [x] Docs
- [x] Tests / harness / CI

## Change Type

- [x] Documentation
- [x] Test / harness

## Verification

Ran:

```text
arXiv API record for 2609.15096 -> title, 18 authors in order, cs.AI, 2026 all match
curl https://doi.org/10.48550/arXiv.2609.15096 -> 302 to https://arxiv.org/abs/2609.15096
CITATION.cff vs the official CFF 1.2.0 JSON schema -> 0 errors (negative control reports its errors)
ruby-cff 1.3.0: validate -> valid; to_bibtex -> @misc, arXiv url, doi, {OpenAI4S Community} braced
mutation pass on the test, 60 variants on scratch copies (each confirmed to have landed):
  the 13 required semantic drifts and 11 more real-drift variants go red
  formatting-only rewrites (rewrap, brace protection, CRLF, field order, @Misc) stay green
  pyproject description / keywords / Source drift -> red
uv run python scripts/check_directory_readmes.py  -> complete bilingual coverage
uv run pre-commit run (changed files)             -> passed
python scripts/source_secret_scan.py              -> passed
uv run python3 -m harness.cli run --tier pr --offline -> 38/38
uv build + scripts/verify_release_artifacts.py    -> passed (CITATION.cff is not in the sdist; no verifier requires it)
full offline suite at 1d48b05e (-n auto --maxprocesses=4 --dist loadfile) -> 9271 passed, 20 skipped
```

Not run:

```text
browser gates; the full suite again after the test-only follow-up commit (the new test file passes on its own)
```

Reason:

```text
No runtime code, route, schema or packaging change.
```

## Risk and Reviewer Focus

Low. `README.md` is also the PyPI long description, so the Citing section will appear on the 0.3.0 PyPI page.

The README BibTeX is kept exactly as arXiv exports it. BibTeX styles will render the unbraced `OpenAI4S Community` as a person ("O. Community") and lower-case "OpenAI4S" in the title. `{OpenAI4S Community}` and `{{OpenAI4S}: …}` would fix both, and the test already accepts that form.

## Checklist

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets.
- [x] No secrets, private data, or local absolute paths are included.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95e71a353d9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
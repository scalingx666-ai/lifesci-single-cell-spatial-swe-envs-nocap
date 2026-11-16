# Issue

**Title:** docs: move to scverse-docs

## Description

Moves the docs to the scverse-doc theme.

- Replace the scanpydoc setup with `scverse_doc` (it provides myst_nb, sphinx-design, autodoc, autosummary, napoleon, intersphinx and copybutton).
- Drop the unused `sphinx_tabs` extension and dependency; the docs already use sphinx-design `tab-set`.
- Drop `needs_sphinx`; `sphinx>=8.1` is in the docs dependencies.
- Add a release note.
- Brighten the link hover color in dark mode (`docs/_static/css/override.css`), since scverse-doc mixes it toward the near-white text color and greys the accent out.

**Colors:** the accent (`#76b900`, NVIDIA green) and secondary accent (`#7400ff`, violet, used for the sidebar captions) are the original RSC brand colors. They are set explicitly in `docs/conf.py` for now and proposed for the website's `accents.json` in scverse/scverse.github.io#377. Once that is merged and scverse-doc is released with it, the explicit values can be dropped and `secondary_accent` set to `True`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `361c395d48d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
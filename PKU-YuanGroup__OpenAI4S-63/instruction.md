# Issue

**Title:** fix(security): an inline gitleaks:allow cannot cover the commit before it

## Description

Found while syncing `next` in #61, whose scan covers **556 commits** against main's 536 and reports one finding `main` never sees:

```
Finding:     content="my api_key=<REDACTED> keep it safe",
RuleID:      generic-api-key
File:        tests/test_share_projection.py
Line:        308
Fingerprint: d8cef1ad…:tests/test_share_projection.py:generic-api-key:308
```

## Why main is green and next is not

The working tree already suppresses this — line 306 carries `# gitleaks:allow`:

```python
# A deliberately fake, secret-SHAPED string to prove _safe_text redacts
# it — not a real credential (gitleaks:allow).
content="my api_key=sk-ABCDEFGH1234567890 keep it safe",  # gitleaks:allow
```

But an inline comment only suppresses the revision that *contains* the comment. The commit that introduced the line **before** anyone added it is still reachable, still scanned, and still flagged. main's history doesn't reach that commit; next's does.

That is the same defect #57 replaced the `.gitleaksignore` fingerprints for, wearing a different hat: **a suppression that describes the present cannot cover history.** So it gets the same treatment — the value joins the anchored `regexTarget = "secret"` allowlist, which covers every revision at once.

## Not a real secret

The string is synthetic by construction and the test says so at the point of use: it is fed through `_safe_text` to prove the share-package projection redacts secret-shaped content. Its 18 trailing characters deliberately fall short of the 24+ that the `sk-` detector in `scripts/source_secret_scan.py` requires, so the two scanners' opposing constraints are both satisfied — the same tension documented for the `tests/test_retrieval_source.py` canary.

The inline comment stays. It is still the clearest signal to someone editing that line, and it costs nothing.

## Consequence for #61

Without this, merging #61 would leave `next`'s own push-scan red — i.e. #61 would not achieve the thing it exists for. #61 needs to be updated from main after this lands.

## Verification

- `uv run pytest tests/test_governance.py` passes; the pinned permitted-value list in `test_gitleaks_config_extends_the_default_rules_rather_than_replacing_them` grows from two entries to three, so the addition had to be made deliberately rather than slipping in.
- `uv run pre-commit run --all-files` passes every hook.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2a82d697147a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
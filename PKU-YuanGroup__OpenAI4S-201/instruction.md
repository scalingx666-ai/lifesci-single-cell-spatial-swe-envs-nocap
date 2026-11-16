# Issue

**Title:** fix(compute): keep the BYOC install id in the configured data dir

## Description

## Summary

BYOC sandbox ownership used `~/.openai4s/install-id` even when the application stored its data elsewhere. A container restart could lose that owner tag and leave running sandboxes unreachable. The resolver now uses `Config.data_dir`, preserves `OPENAI4S_INSTALL_ID` precedence, and copies an existing legacy ID without changing the legacy file.

Concurrent sessions and processes now serialize publication through a retained `.install-id.lock` file and re-read the winner before writing. This also fixes two overwrite races: repairing a corrupt ID and publishing on a filesystem without hard links. Read-permission and other I/O errors preserve the existing file instead of treating it as corrupt. The historical in-memory fallback remains when persistence is unavailable, and its restart limitation is documented.

The offline suite pins the install ID before fixture construction and per test. This branch includes the data-directory isolation changes from #199 and current `main`.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [x] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [x] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Validation on the final source, using the locked Python 3.13 environment with the `science` extra:

```text
uv run --no-sync pytest tests/test_compute_install_id.py tests/test_compute_durability.py tests/test_compute_lifecycle.py
  81 passed
uv run --no-sync python scripts/capture_response_schemas.py --check
  10824 passed, 34 skipped; 215/215 routes exercised; no breaking schema change
uv run --no-sync pre-commit run --all-files
  passed, including strict mypy
uv run --no-sync python scripts/check_directory_readmes.py
  passed: 171 directories, 1744 direct files/assets
uv run --no-sync python scripts/source_secret_scan.py
  passed: 4080 files
uv run --no-sync python -m harness.cli run --tier pr --offline
  38/38 passed
OPENAI4S_SKIP_DOTENV=1 OPENAI4S_INSTALL_ID=offline-pr201-contract uv run --no-sync python scripts/capture_response_contract.py --check
  215/215 routes; contract up to date
```

The three new bug regressions failed before the repair: both concurrent publishers returned different IDs, and a simulated read-permission error replaced an existing owner tag. They pass after the repair. Additional tests start four real processes for fresh, corrupt, and no-hard-link publication, verify recovery after a lock holder is killed, and exercise the Windows locking adapter.

The first full-suite attempt was interrupted after the outer execution sandbox blocked process inspection, R's protocol descriptors, and nested Seatbelt. The complete replacement run uses the suite's normal offline isolation with those OS capabilities available.

Not run locally: live BYOC/SSH jobs, Linux bubblewrap, a native Windows runtime, or browser E2E. This change does not alter the kernel protocol, HTTP routes, or UI. Hosted CI supplies the Linux and browser gates; the Windows adapter test is not a claim of native Windows runtime validation.

## Risk and Reviewer Focus

- `openai4s/compute/manager.py`: resolution precedence, legacy migration, lock lifetime, atomic publication, and preservation of IDs when reads fail. `.install-id.lock` must remain in place so waiting processes continue to coordinate on the same inode.
- `tests/test_compute_install_id.py`: deterministic thread races, real process races, crash recovery, and unreadable-file preservation.
- `tests/conftest.py`: install-ID pinning during collection, fixture setup, and individual tests, alongside #199's data-directory guard.
- Persistence failure retains the previous in-memory fallback; it cannot guarantee ownership across restarts. Operators need a writable/readable data directory or a stable explicit ID.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`, `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. No kernel/composition facade was changed.
- [x] Workbench source and committed dist requirements are satisfied; no workbench changes.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway coverage requirements are satisfied; none of those paths changed.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded where applicable; none were added.
- [x] No new dependencies were added.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Ownership and read-error behavior have synthetic regression coverage.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in the compute and Docker guides.
- [x] English and Chinese Docker guidance and test indexes are synchronized; root READMEs are unchanged.

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Medium Risk**
> Wrong install-id semantics strand live BYOC sandboxes and billing work; migration and race handling are security-relevant for remote compute ownership, though the change is narrowly scoped to resolution/persistence.
>
> **Overview**
> **Persists the BYOC sandbox owner tag under `Config.data_dir`** instead of always using `~/.openai4s/install-id`, so custom `OPENAI4S_DATA_DIR` and container volumes keep the same id across restarts and `reconcile` can still find tagged sandboxes.
>
> Resolution order is now **`OPENAI4S_INSTALL_ID` → `<data_dir>/install-id` → legacy home path (read-only, copied into the data dir on first use) → mint**. Publication uses **`.install-id.lock`**, a re-read under lock, and **hard-link-or-`os.replace`** so concurrent managers agree on one id; empty or invalid stored ids are repaired without overwriting on read-permission failures.
>
> **Docs** (`compute.md`, `docker.md` EN/ZH) describe the new location and drop the Docker “id resets every restart” limitation. **Tests** add `test_compute_install_id.py` and pin `OPENAI4S_INSTALL_ID` in `conftest` so the offline suite does not touch the developer’s real home file.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit d5d8c88be568bcfd9efcf081c20e9cead456c3c8. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19729013fed2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
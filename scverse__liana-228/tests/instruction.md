# Issue

**Title:** Metalinks access

## Description

This pull request updates the version of the `liana` package and improves the reliability of the Metalinks database download process by switching to a GitHub Releases URL. The most significant change is the update to the `_download_metalinksdb` function, which now avoids potential web application firewall (WAF) issues and simplifies the download logic.

Version bump:

* Bumped the package version from `1.7.0` to `1.7.1` in `.bumpversion.cfg`, `pyproject.toml`, and `src/liana/__init__.py` to reflect the new release. [[1]](diffhunk://#diff-9ea6e1e3dde6d4a7e08c7c88eceed69ca745d0d2c779f8f85219b22266efff7fL2-R2) [[2]](diffhunk://#diff-50c86b7ed8ac2cf95bd48334961bf0530cdc77b5a56f852c5c61b89d735fd711L7-R7) [[3]](diffhunk://#diff-bf6faa9057211f6726bddb76f0a6826dd694204f40c8e20587a06ef809bbf396L1-R1)

Resource download reliability:

* Updated the `_download_metalinksdb` function in `src/liana/resource/get_metalinks.py` to use a GitHub Releases URL instead of Figshare, removing the need for custom headers and making the process more CI-friendly and robust against WAF issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `305ea0370781`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
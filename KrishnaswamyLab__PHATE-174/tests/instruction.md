# Issue

**Title:** Add ReadTheDocs configuration for random_landmarking documentation

## Description

The `random_landmarking` parameter is documented in the Python source but not visible on ReadTheDocs. The parameter exists in `PHATE.__init__()` and controls whether landmarks are selected randomly vs. via spectral clustering.

## Changes

- **Added `.readthedocs.yml`**: Explicit build configuration ensures consistent documentation generation across ReadTheDocs environments
  - Python 3.11 build environment
  - Correct installation order (package, then doc dependencies)

- **Fixed `conf.py`**: Changed `language = None` → `language = "en"` to resolve Sphinx warning

- **Fixed `requirements.txt`**: Removed `./Python` line that created circular dependency with ReadTheDocs pip install

The autodoc configuration in `api.rst` already extracts parameter documentation from docstrings. These changes ensure ReadTheDocs builds successfully and includes all documented parameters.

> [!WARNING]
>
> <details>
> <summary>Firewall rules blocked me from connecting to one or more addresses (expand for details)</summary>
>
> #### I tried to connect to the following addresses, but was blocked by firewall rules:
>
> - `phate.readthedocs.io`
>   - Triggering command: `/home/REDACTED/work/_temp/ghcca-node/node/bin/node /home/REDACTED/work/_temp/ghcca-node/node/bin/node --enable-source-maps /home/REDACTED/work/_temp/copilot-developer-action-main/dist/index.js` (dns block)
>
> If you need me to access, download, or install something from one of these locations, you can either:
>
> - Configure [Actions setup steps](https://gh.io/copilot/actions-setup-steps) to set up my environment, which run before the firewall is enabled
> - Add the appropriate URLs or hosts to the custom allowlist in this repository's [Copilot coding agent settings](https://github.com/KrishnaswamyLab/PHATE/settings/copilot/coding_agent) (admins only)
>
> </details>

<!-- START COPILOT ORIGINAL PROMPT -->

<details>

<summary>Original prompt</summary>

>
> ----
>
> *This section details on the original issue you should resolve*
>
> <issue_title>Update PHATE documentation</issue_title>
> <issue_description>PHATE documentation should include random landmarking.</issue_description>
>
> <agent_instructions>The documents are out of date: https://phate.readthedocs.io/en/stable/api.html. You can see this does not mention the new random landmarking feature, for example.
>
> I think you just need to edit this file: https://github.com/KrishnaswamyLab/PHATE/blob/8578022459060e8c29e9b37b537a2203e0c7fd6c/Python/doc/source/api.rst -- But I am not 100% sure.</agent_instructions>
>
> ## Comments on the Issue (you are @copilot in this section)
>
> <comments>
> </comments>
>

</details>

<!-- START COPILOT CODING AGENT SUFFIX -->

- Fixes KrishnaswamyLab/PHATE#173

<!-- START COPILOT CODING AGENT TIPS -->
---

✨ Let Copilot coding agent  — coding agent works faster and does higher quality work when set up for your repo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1694b98cc17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Bump conda-incubator/setup-miniconda from 3.3.0 to 4.0.1 in the actions-deps group

## Description

Bumps the actions-deps group with 1 update: [conda-incubator/setup-miniconda](https://github.com/conda-incubator/setup-miniconda).

Updates `conda-incubator/setup-miniconda` from 3.3.0 to 4.0.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/conda-incubator/setup-miniconda/releases">conda-incubator/setup-miniconda's releases</a>.</em></p>
<blockquote>
<h2>Version 4.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix MultipleKeysError when user condarc declares auto_activate by <a href="https://github.com/jezdez"><code>@​jezdez</code></a> in <a href="">conda-incubator/setup-miniconda#500</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/conda-incubator/setup-miniconda/compare/v4.0.0...v4.0.1">https://github.com/conda-incubator/setup-miniconda/compare/v4.0.0...v4.0.1</a></p>
<h2>Version 4.0.0</h2>
<h3>Breaking Changes</h3>
<ul>
<li><a href="">#459</a>: Upgrade action runtime to Node.js 24.x (requires runners with
Node 24 support; this is the reason for the v4 major bump)</li>
<li><a href="">#450</a>: Switch action build to ESM (for <code>@actions/exec</code> v3)</li>
</ul>
<h3>Features and Enhancements</h3>
<ul>
<li><a href="">#469</a>: Add <code>conda-init</code> input to optionally skip <code>conda init</code> and
document activation for restricted environments</li>
<li><a href="">#482</a>: Add channels parsing utility and URL validation</li>
<li><a href="">#481</a>: Enable stricter TypeScript checks and typing</li>
<li><a href="">#480</a>: Add more tests, increase coverage, add Codecov integration and
coverage badge</li>
<li><a href="">#479</a>: Add TypeDoc-based API docs, generation and checks; configure
GitHub Pages and Netlify previews</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><a href="">#465</a>: Fix double channel configuration being applied</li>
<li><a href="">#467</a>: Speed up Windows post-run cleanup by moving the extracted
packages directory instead of removing files one by one</li>
<li><a href="">#470</a>: Fix <code>name-version-build</code> syntax expansion and add tests</li>
<li><a href="">#475</a>: Split shell init and activation of the test environment to remove
spurious warning</li>
<li><a href="">#498</a>: Skip Netlify preview for Dependabot PRs</li>
</ul>
<h3>Performance</h3>
<ul>
<li><a href="">#486</a>: Remove HTML index scraping for Miniconda version validation</li>
<li><a href="">#487</a>: Parallelize Windows <code>takeown</code> calls with <code>Promise.all</code></li>
<li><a href="">#488</a>: Replace <code>isDefaultEnvironment</code> subprocess with local YAML reads</li>
<li><a href="">#489</a>: Replace <code>conda config</code> subprocesses with direct <code>.condarc</code> YAML
writes</li>
</ul>
<h3>Tasks and Maintenance</h3>
<ul>
<li><a href="">#444</a>: Bump conda-incubator/setup-miniconda from 3.2.0 to 3.3.0</li>
<li><a href="">#445</a>: Bump actions/checkout from 6.0.1 to 6.0.2</li>
<li><a href="">#449</a>: Bump <code>@​actions/exec</code> from 2.0.0 to 3.0.0</li>
<li><a href="">#456</a>, <a href="">#484</a>, <a href="">#491</a>: Bump actions/upload-artifact</li>
<li><a href="">#460</a>: Bump actions/download-artifact from 7.0.0 to 8.0.1</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/conda-incubator/setup-miniconda/blob/main/CHANGELOG.md">conda-incubator/setup-miniconda's changelog</a>.</em></p>
<blockquote>
<h1>CHANGELOG</h1>
<h2><a href="https://github.com/conda-incubator/setup-miniconda/releases/tag/v4.0.1">v4.0.1</a> (2026-04-24)</h2>
<h3>Fixes</h3>
<ul>
<li>Fix <code>MultipleKeysError</code> on conda 25.11+ when a user-supplied <code>condarc-file</code>
already declares <code>auto_activate</code>: now only one of <code>auto_activate</code> /
<code>auto_activate_base</code> is written to <code>.condarc</code>, preferring whichever key the
user's existing condarc uses.</li>
<li>Add <code>auto_activate</code> to the boolean coercion set so its value is serialized as
a YAML boolean when it is the chosen canonical key.</li>
<li>Add <code>local_repodata_ttl</code> to <code>KNOWN_CONDARC_KEYS</code> to silence a spurious
&quot;Unrecognized condarc key&quot; warning for a valid conda key.</li>
</ul>
<h2>[v4.0.0] (2026-04-23)</h2>
<h3>Breaking Changes</h3>
<ul>
<li><a href="">#459</a>[459]: Upgrade action runtime to Node.js 24.x (requires runners with
Node 24 support; this is the reason for the v4 major bump)</li>
<li><a href="">#450</a>[450]: Switch action build to ESM (for <code>@actions/exec</code> v3)</li>
</ul>
<h3>Features and Enhancements</h3>
<ul>
<li><a href="">#469</a>[469]: Add <code>conda-init</code> input to optionally skip <code>conda init</code> and
document activation for restricted environments</li>
<li><a href="">#482</a>[482]: Add channels parsing utility and URL validation</li>
<li><a href="">#481</a>[481]: Enable stricter TypeScript checks and typing</li>
<li><a href="">#480</a>[480]: Add more tests, increase coverage, add Codecov integration and
coverage badge</li>
<li><a href="">#479</a>[479]: Add TypeDoc-based API docs, generation and checks; configure
GitHub Pages and Netlify previews</li>
</ul>
<h3>Fixes</h3>
<ul>
<li><a href="">#465</a>[465]: Fix double channel configuration being applied</li>
<li><a href="">#467</a>[467]: Speed up Windows post-run cleanup by moving the extracted
packages directory instead of removing files one by one</li>
<li><a href="">#470</a>[470]: Fix <code>name-version-build</code> syntax expansion and add tests</li>
<li><a href="">#475</a>[475]: Split shell init and activation of the test environment to remove
spurious warning</li>
</ul>
<h3>Performance</h3>
<ul>
<li><a href="">#486</a>[486]: Remove HTML index scraping for Miniconda version validation</li>
<li><a href="">#487</a>[487]: Parallelize Windows <code>takeown</code> calls with <code>Promise.all</code></li>
<li><a href="">#488</a>[488]: Replace <code>isDefaultEnvironment</code> subprocess with local YAML reads</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8ee1f36</code></a> Fix MultipleKeysError when user condarc declares auto_activate (<a href="">#500</a>)</li>
<li><a href=""><code>bce0bd8</code></a> Prepare v4 release (<a href="">#499</a>)</li>
<li><a href=""><code>78fb0ff</code></a> ci(docs): skip Netlify preview for Dependabot PRs (<a href="">#498</a>)</li>
<li><a href=""><code>d32e72e</code></a> Bump <code>@​actions/core</code> from 3.0.0 to 3.0.1 (<a href="">#496</a>)</li>
<li><a href=""><code>3e251ae</code></a> Bump actions/upload-artifact from 4 to 7 (<a href="">#491</a>)</li>
<li><a href=""><code>7ff02ae</code></a> Bump actions/upload-pages-artifact from 3 to 5 (<a href="">#492</a>)</li>
<li><a href=""><code>65b62b8</code></a> Bump actions/deploy-pages from 4 to 5 (<a href="">#494</a>)</li>
<li><a href=""><code>1eb4d38</code></a> Bump marocchino/sticky-pull-request-comment from 2 to 3 (<a href="">#493</a>)</li>
<li><a href=""><code>bfb6f7e</code></a> Bump codecov/codecov-action from 5 to 6 (<a href="">#495</a>)</li>
<li><a href=""><code>77236ef</code></a> Merge pull request <a href="">#489</a> from conda-incubator/perf/direct-condarc-write</li>
<li>Additional commits viewable in <a href="https://github.com/conda-incubator/setup-miniconda/compare/fc2d68f6413eb2d87b895e92f8584b5b94a10167...8ee1f361103df19b6f8c8655fd3967a8ecb162d5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=conda-incubator/setup-miniconda&package-manager=github_actions&previous-version=3.3.0&new-version=4.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e57587c216cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
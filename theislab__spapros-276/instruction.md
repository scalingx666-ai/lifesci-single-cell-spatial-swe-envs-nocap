# Issue

**Title:** [DEPENDABOT]: Bump safety from 1.10.3 to 2.3.5

## Description

Bumps [safety](https://github.com/pyupio/safety) from 1.10.3 to 2.3.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pyupio/safety/releases">safety's releases</a>.</em></p>
<blockquote>
<h2>2.3.5</h2>
<p>No release notes provided.</p>
<h2>2.3.4</h2>
<p>No release notes provided.</p>
<h2>2.3.3</h2>
<p>No release notes provided.</p>
<h2>2.3.2</h2>
<ul>
<li>Fixed <a href="">#423</a>: Bare output includes extra line in non-screen output with no vulnerabilities.</li>
<li>Fixed <a href="">#422</a>: ResourceWarning (unclosed socket) in safety v.2.3.1.</li>
<li>Fixed telemetry data missing when the CLI mode is used.</li>
<li>Fixed wrong database fetching when the KEY and the database arguments are used at the same time.</li>
<li>Added SAFETY_PURE_YAML env var, used for cases that require pure Python in the YAML parser.</li>
</ul>
<h2>2.3.1</h2>
<p>No release notes provided.</p>
<h2>2.3.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Safety Alerts: GitHub PRs and GitHub issues support by <a href="https://github.com/cb22"><code>@​cb22</code></a> in <a href="">pyupio/safety#411</a></li>
<li>Safety 2.3.0 patch by <a href="https://github.com/cb22"><code>@​cb22</code></a> in <a href="">pyupio/safety#415</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pyupio/safety/compare/2.2.1...2.3.0">https://github.com/pyupio/safety/compare/2.2.1...2.3.0</a></p>
<h2>2.2.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Pull from Master by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#410</a></li>
<li>Common fixes for next release by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#412</a></li>
<li>2.2.1 Patch by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#414</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pyupio/safety/compare/2.2.0...2.2.1">https://github.com/pyupio/safety/compare/2.2.0...2.2.1</a></p>
<h2>2.2.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Eat stderr messages from git commands. by <a href="https://github.com/tarmack"><code>@​tarmack</code></a> in <a href="">pyupio/safety#399</a></li>
<li>Update from master branch by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#404</a></li>
<li>Remove AppVeyor and Travis by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#405</a></li>
<li>Using dparse to read requirements and fixes for custom integrations by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#406</a></li>
<li>Safety 2.2.0 patch by <a href="https://github.com/yeisonvargasf"><code>@​yeisonvargasf</code></a> in <a href="">pyupio/safety#407</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/tarmack"><code>@​tarmack</code></a> made their first contribution in <a href="">pyupio/safety#399</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pyupio/safety/compare/2.1.1...2.2.0">https://github.com/pyupio/safety/compare/2.1.1...2.2.0</a></p>
<h2>Safety 2.0.0 and Safety GitHub Action - Python Dependency Scanner</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pyupio/safety/blob/main/CHANGELOG.md">safety's changelog</a>.</em></p>
<blockquote>
<h2>[2.3.5] - 2022-12-08</h2>
<ul>
<li>Pinned packaging dependency to a compatible range.</li>
<li>Pinned the CI actions to the runner image with Python 3.6 support.</li>
</ul>
<h2>[2.3.4] - 2022-12-07</h2>
<ul>
<li>Removed LegacyVersion use; this fixes the issue with packaging 22.0.</li>
<li>Fixed typos in the README.</li>
<li>Added Python 3.11 to the classifiers in the setup.cfg.</li>
</ul>
<h2>[2.3.3] - 2022-11-27</h2>
<ul>
<li>Fixed recursive requirements issue when an unpinned package is found.</li>
</ul>
<h2>[2.3.2] - 2022-11-21</h2>
<ul>
<li>Fixed <a href="">#423</a>: Bare output includes extra line in non-screen output with no vulnerabilities.</li>
<li>Fixed <a href="">#422</a>: ResourceWarning (unclosed socket) in safety v.2.3.1.</li>
<li>Fixed telemetry data missing when the CLI mode is used.</li>
<li>Fixed wrong database fetching when the KEY and the database arguments are used at the same time.</li>
<li>Added <code>SAFETY_PURE_YAML</code> env var, used for cases that require pure Python in the YAML parser.</li>
</ul>
<h2>[2.3.1] - 2022-10-05</h2>
<ul>
<li>Add <code>safety.alerts</code> module to setup.cfg</li>
</ul>
<h2>[2.3.0] - 2022-10-05</h2>
<ul>
<li>Safety can now create GitHub PRs and Issues for vulnerabilities directly, with the new <code>safety alert</code> subcommand.</li>
<li>Support for GitHub PR and Issue alerting has been added to the GitHub Action.</li>
</ul>
<h2>[2.2.1] - 2022-10-04</h2>
<ul>
<li>Fixed the use of the SAFETY_COLOR environment variable</li>
<li>Fixed bug in the case of vulnerabilities without a CVE linked</li>
<li>Fixed GitHub version in the README</li>
</ul>
<h2>[2.2.0] - 2022-09-19</h2>
<ul>
<li>Safety starts to use dparse to parse files, now Safety supports mainly Poetry and Pipenv lock files plus other files supported by dparse.</li>
<li>Added logic for custom integrations like pipenv check.</li>
<li>The --db flag is compatible remote sources too.</li>
<li>Added more logging</li>
<li>Upgrade dparse dependency to avoid a possible ReDos security issue</li>
<li>Removed Travis and Appveyor, the CI/CD was migrated to GitHub Actions</li>
</ul>
<h2>[2.1.1] - 2022-07-18</h2>
<ul>
<li>Fix crash when running on systems without git present (Thanks <a href="https://github.com/andyjones"><code>@​andyjones</code></a>)</li>
</ul>
<h2>[2.1.0] - 2022-07-14</h2>
<h3>Summary:</h3>
<ul>
<li>Improved error messages &amp; fixed issues with proxies</li>
<li>Fixed license command</li>
<li>Added the ability for scan outputs to be sent to pyup.io. This will only take effect if using an API key, the feature is enabled on your profile, and the <code>--disable-audit-and-monitor</code> is not set</li>
<li>Added the ability to have a Safety policy file set centrally on your pyup.io profile. This remote policy file will be used if there's no local policy file present, otherwise a warning will be issued.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d8bd6f7</code></a> Version 2.3.5</li>
<li><a href=""><code>a10fbd8</code></a> Merge pull request <a href="">#444</a> from pyupio/develop</li>
<li><a href=""><code>7b24998</code></a> Test integration for 2.3.4</li>
<li><a href=""><code>7d6dd5e</code></a> Update the OS mapping in the binaries file.</li>
<li><a href=""><code>b62b75c</code></a> Merge pull request <a href="">#443</a> from pyupio/fix/pin-compatible-packaging-versions</li>
<li><a href=""><code>93598ae</code></a> Pin the ubuntu version to be used for the CI.</li>
<li><a href=""><code>aa1b153</code></a> Use packaging versions &lt; 22.0 to prevent issues.</li>
<li><a href=""><code>f78823c</code></a> Starting version 2.3.5.dev</li>
<li><a href=""><code>9164106</code></a> Merge pull request <a href="">#442</a> from pyupio/main</li>
<li><a href=""><code>46d54bc</code></a> Version 2.3.4</li>
<li>Additional commits viewable in <a href="https://github.com/pyupio/safety/compare/1.10.3...2.3.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=safety&package-manager=pip&previous-version=1.10.3&new-version=2.3.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d255b6d5f3e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
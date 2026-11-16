# Issue

**Title:** ci(dependabot): bump codecov/codecov-action from 4 to 5 in the actions group

## Description

Bumps the actions group with 1 update: [codecov/codecov-action](https://github.com/codecov/codecov-action).

Updates `codecov/codecov-action` from 4 to 5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v5.0.0</h2>
<h2>v5 Release</h2>
<p><code>v5</code> of the Codecov GitHub Action will use the <a href="https://github.com/codecov/wrapper">Codecov Wrapper</a> to encapsulate the <a href="https://github.com/codecov/codecov-cli">CLI</a>. This will help ensure that the Action gets updates quicker.</p>
<h3>Migration Guide</h3>
<p>The <code>v5</code> release also coincides with the opt-out feature for tokens for public repositories. In the <code>Global Upload Token</code> section of the settings page of an organization in codecov.io, you can set the ability for Codecov to receive a coverage reports from any source. This will allow contributors or other members of a repository to upload without needing access to the Codecov token. For more details see <a href="https://docs.codecov.com/docs/codecov-tokens#uploading-without-a-token">how to upload without a token</a>.</p>
<blockquote>
<p>[!WARNING]<br />
<strong>The following arguments have been changed</strong></p>
<ul>
<li><code>file</code> (this has been deprecated in favor of <code>files</code>)</li>
<li><code>plugin</code> (this has been deprecated in favor of <code>plugins</code>)</li>
</ul>
</blockquote>
<p>The following arguments have been added:</p>
<ul>
<li><code>binary</code></li>
<li><code>gcov_args</code></li>
<li><code>gcov_executable</code></li>
<li><code>gcov_ignore</code></li>
<li><code>gcov_include</code></li>
<li><code>report_type</code></li>
<li><code>skip_validation</code></li>
<li><code>swift_project</code></li>
</ul>
<p>You can see their usage in the <code>action.yml</code> <a href="https://github.com/codecov/codecov-action/blob/main/action.yml">file</a>.</p>
<h2>What's Changed</h2>
<ul>
<li>chore(deps): bump to eslint9+ and remove eslint-config-google by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1591</a></li>
<li>build(deps-dev): bump <code>@​octokit/webhooks-types</code> from 7.5.1 to 7.6.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1595</a></li>
<li>build(deps-dev): bump typescript from 5.6.2 to 5.6.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1604</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1601</a></li>
<li>build(deps): bump <code>@​actions/core</code> from 1.11.0 to 1.11.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1597</a></li>
<li>build(deps): bump github/codeql-action from 3.26.9 to 3.26.11 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1596</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1600</a></li>
<li>build(deps-dev): bump eslint from 9.11.1 to 9.12.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1598</a></li>
<li>build(deps): bump github/codeql-action from 3.26.11 to 3.26.12 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1609</a></li>
<li>build(deps): bump actions/checkout from 4.2.0 to 4.2.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1608</a></li>
<li>build(deps): bump actions/upload-artifact from 4.4.0 to 4.4.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1607</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.8.1 to 8.9.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1612</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.8.1 to 8.9.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1611</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.9.0 to 8.10.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1615</a></li>
<li>build(deps-dev): bump eslint from 9.12.0 to 9.13.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1618</a></li>
<li>build(deps): bump github/codeql-action from 3.26.12 to 3.26.13 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1617</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.9.0 to 8.10.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1614</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.10.0 to 8.11.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1620</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.10.0 to 8.11.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1619</a></li>
<li>build(deps-dev): bump <code>@​types/jest</code> from 29.5.13 to 29.5.14 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1622</a></li>
<li>build(deps): bump actions/checkout from 4.2.1 to 4.2.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1625</a></li>
<li>build(deps): bump github/codeql-action from 3.26.13 to 3.27.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1624</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.11.0 to 8.12.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1626</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.12.1 to 8.12.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1629</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/main/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h3>v5 Release</h3>
<p><code>v5</code> of the Codecov GitHub Action will use the <a href="https://github.com/codecov/wrapper">Codecov Wrapper</a> to encapsulate the <a href="https://github.com/codecov/codecov-cli">CLI</a>. This will help ensure that the Action gets updates quicker.</p>
<h3>Migration Guide</h3>
<p>The <code>v5</code> release also coincides with the opt-out feature for tokens for public repositories. In the <code>Global Upload Token</code> section of the settings page of an organization in codecov.io, you can set the ability for Codecov to receive a coverage reports from any source. This will allow contributors or other members of a repository to upload without needing access to the Codecov token. For more details see <a href="https://docs.codecov.com/docs/codecov-tokens#uploading-without-a-token">how to upload without a token</a>.</p>
<blockquote>
<p>[!WARNING]
<strong>The following arguments have been changed</strong></p>
<ul>
<li><code>file</code> (this has been deprecated in favor of <code>files</code>)</li>
<li><code>plugin</code> (this has been deprecated in favor of <code>plugins</code>)</li>
</ul>
</blockquote>
<p>The following arguments have been added:</p>
<ul>
<li><code>binary</code></li>
<li><code>gcov_args</code></li>
<li><code>gcov_executable</code></li>
<li><code>gcov_ignore</code></li>
<li><code>gcov_include</code></li>
<li><code>report_type</code></li>
<li><code>skip_validation</code></li>
<li><code>swift_project</code></li>
</ul>
<p>You can see their usage in the <code>action.yml</code> <a href="https://github.com/codecov/codecov-action/blob/main/action.yml">file</a>.</p>
<h2>What's Changed</h2>
<ul>
<li>chore(deps): bump to eslint9+ and remove eslint-config-google by <a href="https://github.com/thomasrockhu-codecov"><code>@​thomasrockhu-codecov</code></a> in <a href="">codecov/codecov-action#1591</a></li>
<li>build(deps-dev): bump <code>@​octokit/webhooks-types</code> from 7.5.1 to 7.6.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1595</a></li>
<li>build(deps-dev): bump typescript from 5.6.2 to 5.6.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1604</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1601</a></li>
<li>build(deps): bump <code>@​actions/core</code> from 1.11.0 to 1.11.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1597</a></li>
<li>build(deps): bump github/codeql-action from 3.26.9 to 3.26.11 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1596</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.8.0 to 8.8.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1600</a></li>
<li>build(deps-dev): bump eslint from 9.11.1 to 9.12.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1598</a></li>
<li>build(deps): bump github/codeql-action from 3.26.11 to 3.26.12 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1609</a></li>
<li>build(deps): bump actions/checkout from 4.2.0 to 4.2.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1608</a></li>
<li>build(deps): bump actions/upload-artifact from 4.4.0 to 4.4.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1607</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.8.1 to 8.9.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1612</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.8.1 to 8.9.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1611</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.9.0 to 8.10.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1615</a></li>
<li>build(deps-dev): bump eslint from 9.12.0 to 9.13.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1618</a></li>
<li>build(deps): bump github/codeql-action from 3.26.12 to 3.26.13 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1617</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.9.0 to 8.10.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1614</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.10.0 to 8.11.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1620</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.10.0 to 8.11.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1619</a></li>
<li>build(deps-dev): bump <code>@​types/jest</code> from 29.5.13 to 29.5.14 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1622</a></li>
<li>build(deps): bump actions/checkout from 4.2.1 to 4.2.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1625</a></li>
<li>build(deps): bump github/codeql-action from 3.26.13 to 3.27.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1624</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.11.0 to 8.12.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1626</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.12.1 to 8.12.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1629</a></li>
<li>build(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.11.0 to 8.12.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">codecov/codecov-action#1628</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>015f24e</code></a> chore(release): 5.0.7 (<a href="">#1691</a>)</li>
<li><a href=""><code>a76271d</code></a> fix: use HEAD_REPO (<a href="">#1690</a>)</li>
<li><a href=""><code>d168679</code></a> chore(release): 5.0.6 (<a href="">#1689</a>)</li>
<li><a href=""><code>373fd71</code></a> fix: update CODECOV_TOKEN and fix tokenless (<a href="">#1688</a>)</li>
<li><a href=""><code>288befb</code></a> chore(release): 5.0.5 (<a href="">#1686</a>)</li>
<li><a href=""><code>7e69d37</code></a> chore(release): wrapper-0.0.27 (<a href="">#1685</a>)</li>
<li><a href=""><code>985343d</code></a> chore(release): 5.0.4 (<a href="">#1682</a>)</li>
<li><a href=""><code>31d1900</code></a> chore(deps): bump wrapper to 0.0.26 (<a href="">#1681</a>)</li>
<li><a href=""><code>095cfe0</code></a> fix: strip out a trailing /n from input tokens (<a href="">#1679</a>)</li>
<li><a href=""><code>b542d5a</code></a> fix: add action version (<a href="">#1678</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v4...v5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=4&new-version=5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3ae66c325d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
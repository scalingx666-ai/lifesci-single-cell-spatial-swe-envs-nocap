# Issue

**Title:** build(deps): bump docker/login-action from 4.7.0 to 4.8.0 in the github-actions-patch-minor group

## Description

Bumps the github-actions-patch-minor group with 1 update: [docker/login-action](https://github.com/docker/login-action).

Updates `docker/login-action` from 4.7.0 to 4.8.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.8.0</h2>
<ul>
<li>Set Docker Hub OIDC token lifetime default to 1 hour by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1070</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> and <code>@​aws-sdk/client-ecr-public</code> to 3.1161.0 in <a href="">docker/login-action#1103</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.107.0 to 0.109.0 in <a href="">docker/login-action#1105</a></li>
<li>Bump vite from 7.3.6 to 7.3.7 in <a href="">docker/login-action#1101</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.7.0...v4.8.0">https://github.com/docker/login-action/compare/v4.7.0...v4.8.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8aa5831</code></a> Merge pull request <a href="">#1105</a> from docker/dependabot/npm_and_yarn/docker/actions-t...</li>
<li><a href=""><code>043f81d</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>3ff6998</code></a> build(deps): bump <code>@​docker/actions-toolkit</code> from 0.107.0 to 0.109.0</li>
<li><a href=""><code>694ef6a</code></a> Merge pull request <a href="">#1103</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependen...</li>
<li><a href=""><code>7c6e412</code></a> [dependabot skip] chore: update generated content</li>
<li><a href=""><code>aa2441f</code></a> build(deps): bump the aws-sdk-dependencies group across 1 directory with 2 up...</li>
<li><a href=""><code>d6c10b0</code></a> Merge pull request <a href="">#1106</a> from docker/dependabot/github_actions/codeql-actions...</li>
<li><a href=""><code>319f1ee</code></a> Merge pull request <a href="">#1104</a> from docker/dependabot/github_actions/actions/setup-...</li>
<li><a href=""><code>b483b7f</code></a> Merge pull request <a href="">#1101</a> from docker/dependabot/npm_and_yarn/vite-7.3.7</li>
<li><a href=""><code>dc7d67c</code></a> Merge pull request <a href="">#1070</a> from crazy-max/increase-oidc-default-expiry</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/81c6f93d4bc991e510b342a00b419b3bb4efc5c6...8aa5831fb8d48d8f76594c7ddde61ae58019f550">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=docker/login-action&package-manager=github_actions&previous-version=4.7.0&new-version=4.8.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1baee6b19a8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
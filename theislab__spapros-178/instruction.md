# Issue

**Title:** [DEPENDABOT]: Bump actions/checkout from 2.3.4 to 2.4.0

## Description

Bumps [actions/checkout](https://github.com/actions/checkout) from 2.3.4 to 2.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v2.4.0</h2>
<ul>
<li>Convert SSH URLs like <code>org-&lt;ORG_ID&gt;@github.com:</code> to <code>https://github.com/</code> - <a href="https://github-redirect.dependabot.com/actions/checkout/pull/621">pr</a></li>
</ul>
<h2>v2.3.5</h2>
<p>Update dependencies</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ec3a7ce</code></a> set insteadOf url for org-id (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/621">#621</a>)</li>
<li><a href=""><code>fd47087</code></a> codeql should analyze lib not dist (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/620">#620</a>)</li>
<li><a href=""><code>3d677ac</code></a> script to generate license info (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/614">#614</a>)</li>
<li><a href=""><code>826ba42</code></a> npm audit fix (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/612">#612</a>)</li>
<li><a href=""><code>eb8a193</code></a> update dev dependencies and react to new linting rules (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/611">#611</a>)</li>
<li><a href=""><code>c49af7c</code></a> Create codeql-analysis.yml (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/602">#602</a>)</li>
<li><a href=""><code>1e204e9</code></a> update licensed check (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/606">#606</a>)</li>
<li><a href=""><code>0299a0d</code></a> update dist (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/605">#605</a>)</li>
<li><a href=""><code>be0f448</code></a> Bump ws from 5.2.2 to 5.2.3 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/604">#604</a>)</li>
<li><a href=""><code>56c00a7</code></a> Bump tmpl from 1.0.4 to 1.0.5 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/588">#588</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/checkout/compare/v2.3.4...v2.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/checkout&package-manager=github_actions&previous-version=2.3.4&new-version=2.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcb38e4c3e92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
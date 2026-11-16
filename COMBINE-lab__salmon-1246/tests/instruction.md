# Issue

**Title:** chore(deps): bump zod from 4.6.5 to 4.6.7 in /website

## Description

Bumps [zod](https://github.com/colinhacks/zod) from 4.6.5 to 4.6.7.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/colinhacks/zod/releases">zod's releases</a>.</em></p>
<blockquote>
<h2>v4.6.7</h2>
<h2>Commits:</h2>
<ul>
<li>b500a2ee95134f81d74da7911d7378dd2853d042 4.6.7</li>
</ul>
<h2>v4.6.6</h2>
<blockquote>
<p>Six malicious commits pushed to <code>main</code> on September 21 with a compromised git credential were reverted the same day in <a href="">#6620</a> and have since been removed from the history of <code>main</code>. None were ever published to npm. The npm provenance for 4.6.6 names 284243fb, the pre-rewrite copy of 9c219833 with identical contents.</p>
</blockquote>
<h2>Commits:</h2>
<ul>
<li>0cd3af5e9f50ad11bbcd4407a46a21b8848ba574 docs: load the en locale directly in Zod Mini</li>
<li>9d5e60f162997b764b40d45aa02481888db50dea docs: import locales from zod/locales, not z.locales</li>
<li>34a626f307871ecbb0123947559328dc52ed5e3e docs: tighten the z.locales tree-shaking note</li>
<li>74304ce5b5796b5edb9a88ceb8e170b6ea3e82df release: stage npm versions instead of publishing them (<a href="">#6622</a>)</li>
<li>b2ef983e0711ff6517d6020b021071e2e5653efa docs: add Code for Japan to bronze sponsors</li>
<li>8fb2faf0584828a6a027d8279db36f6f52784462 docs: crop the Code for Japan logo and list it first in bronze</li>
<li>bacad518c41610d654658172d325874bf0ee6290 docs: square the Code for Japan logo to match the other bronze tiles</li>
<li>c42596bd1c87e941d7241d10e012c5c196adcc10 release: hold the run on the release-approval environment until the staged versions are approved (<a href="">#6638</a>)</li>
<li>a2ba4a67986a3e6b2b131be30084a2f460d9ea67 fix(types): declare record output and input as members, not base type arguments (<a href="">#6645</a>)</li>
<li>a0ebf970f2d752e5f58527cd2942ff48be4f46bd fix(v4): check array, set and map size bounds before parsing elements (<a href="">#6652</a>)</li>
<li>529f78dd9431b07f49647fee3aa0819b3f8b66b7 4.6.6</li>
<li>9c219833c3a3764fa1f1ea9c5ecec8254a63c0b1 ci: stage at verbose so a failed OIDC token exchange says why</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b500a2e</code></a> 4.6.7</li>
<li><a href=""><code>9c21983</code></a> ci: stage at verbose so a failed OIDC token exchange says why</li>
<li><a href=""><code>529f78d</code></a> 4.6.6</li>
<li><a href=""><code>a0ebf97</code></a> fix(v4): check array, set and map size bounds before parsing elements (<a href="">#6652</a>)</li>
<li><a href=""><code>a2ba4a6</code></a> fix(types): declare record output and input as members, not base type argumen...</li>
<li><a href=""><code>c42596b</code></a> release: hold the run on the release-approval environment until the staged ve...</li>
<li><a href=""><code>bacad51</code></a> docs: square the Code for Japan logo to match the other bronze tiles</li>
<li><a href=""><code>8fb2faf</code></a> docs: crop the Code for Japan logo and list it first in bronze</li>
<li><a href=""><code>b2ef983</code></a> docs: add Code for Japan to bronze sponsors</li>
<li><a href=""><code>74304ce</code></a> release: stage npm versions instead of publishing them (<a href="">#6622</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/colinhacks/zod/compare/v4.6.5...v4.6.7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=zod&package-manager=npm_and_yarn&previous-version=4.6.5&new-version=4.6.7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e461104506f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
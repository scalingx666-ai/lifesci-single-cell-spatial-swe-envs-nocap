# Issue

**Title:** chore(deps): bump nanoid from 3.1.25 to 3.3.1 in /client

## Description

Bumps [nanoid](https://github.com/ai/nanoid) from 3.1.25 to 3.3.1.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/ai/nanoid/blob/main/CHANGELOG.md">nanoid's changelog</a>.</em></p>
<blockquote>
<h2>3.3.1</h2>
<ul>
<li>Reduced package size.</li>
</ul>
<h2>3.3</h2>
<ul>
<li>Added <code>size</code> argument to function from <code>customAlphabet</code> (by Stefan Sundin).</li>
</ul>
<h2>3.2</h2>
<ul>
<li>Added <code>--size</code> and <code>--alphabet</code> arguments to binary (by Vitaly Baev).</li>
</ul>
<h2>3.1.32</h2>
<ul>
<li>Reduced <code>async</code> exports size (by Artyom Arutyunyan).</li>
<li>Moved from Jest to uvu (by Vitaly Baev).</li>
</ul>
<h2>3.1.31</h2>
<ul>
<li>Fixed collision vulnerability on object in <code>size</code> (by Artyom Arutyunyan).</li>
</ul>
<h2>3.1.30</h2>
<ul>
<li>Reduced size for project with <code>brotli</code> compression (by Anton Khlynovskiy).</li>
</ul>
<h2>3.1.29</h2>
<ul>
<li>Reduced npm package size.</li>
</ul>
<h2>3.1.28</h2>
<ul>
<li>Reduced npm package size.</li>
</ul>
<h2>3.1.27</h2>
<ul>
<li>Cleaned <code>dependencies</code> from development tools.</li>
</ul>
<h2>3.1.26</h2>
<ul>
<li>Improved performance (by Eitan Har-Shoshanim).</li>
<li>Reduced npm package size.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ec6f809</code></a> Release 3.3.1 version</li>
<li><a href=""><code>c7d8578</code></a> Update dependencies</li>
<li><a href=""><code>05b2596</code></a> Remove old tests</li>
<li><a href=""><code>368a6e7</code></a> Remove process.env.NODE_ENV</li>
<li><a href=""><code>ee7dee3</code></a> Remove <code>@​napi-rs/uuid</code> to fix CI</li>
<li><a href=""><code>defe20f</code></a> Try to fix CI</li>
<li><a href=""><code>ee85121</code></a> Try to fix CI</li>
<li><a href=""><code>c7f4219</code></a> Sync English and Russian docs</li>
<li><a href=""><code>f74a41d</code></a> Release 3.3 version</li>
<li><a href=""><code>9c09cdc</code></a> Fix coverage config</li>
<li>Additional commits viewable in <a href="https://github.com/ai/nanoid/compare/3.1.25...3.3.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=nanoid&package-manager=npm_and_yarn&previous-version=3.1.25&new-version=3.3.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot use these labels` will set the current labels as the default for future PRs for this repo and language
- `@dependabot use these reviewers` will set the current reviewers as the default for future PRs for this repo and language
- `@dependabot use these assignees` will set the current assignees as the default for future PRs for this repo and language
- `@dependabot use this milestone` will set the current milestone as the default for future PRs for this repo and language

You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/chanzuckerberg/cellxgene/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38fdc649f558`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
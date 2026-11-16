# Issue

**Title:** build(deps): bump pypa/gh-action-pypi-publish from 1.14.2 to 1.14.3

## Description

Bumps [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) from 1.14.2 to 1.14.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/gh-action-pypi-publish/releases">pypa/gh-action-pypi-publish's releases</a>.</em></p>
<blockquote>
<h2>v1.14.3</h2>
<!-- raw HTML omitted -->
<blockquote>
<p>[!important]
🚨 This release includes fixes for <a href="https://github.com/pypa/gh-action-pypi-publish/security/advisories/GHSA-5xjx-3w67-w9x9">GHSA-5xjx-3w67-w9x9</a> patched up by <a href="https://github.com/sethmlarson"><code>@​sethmlarson</code></a><a href="https://github.com/sponsors/sethmlarson">💰</a> in <a href="">#427</a> and in other places across the ecosystem.</p>
<p>Additional ecosystem and related mitigations beyond you might want to watch out for:</p>
<ul>
<li><a href="https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576">https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576</a></li>
<li><a href="https://emudhra.we-have-a-problem.com">https://emudhra.we-have-a-problem.com</a></li>
</ul>
</blockquote>
<h2>🛠️ Security Tightening</h2>
<p><a href="https://github.com/webknjaz"><code>@​webknjaz</code></a><a href="https://github.com/sponsors/webknjaz">💰</a> made sure the dependency tree within the action runtime uses hash-checking from now on via <a href="">pypa/gh-action-pypi-publish#420</a>.</p>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.2...v1.14.3">https://github.com/pypa/gh-action-pypi-publish/compare/v1.14.2...v1.14.3</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz</code></a> <a href="https://stand-with-ukraine.pp.ua">🇺🇦</a></p>
<p><strong>💬 Discuss</strong> <a href="https://bsky.app/profile/webknjaz.me/post/3mydcjweyak2f">on Bluesky 🦋</a>, <a href="https://mastodon.social/@webknjaz/117474743338290807">on Mastodon 🐘</a> and <a href="https://github.com/pypa/gh-action-pypi-publish/discussions/429">on GitHub</a>.</p>
<p><a href="https://github.com/sponsors/webknjaz"><img src="https://img.shields.io/badge/%40webknjaz-transparent?logo=githubsponsors&amp;logoColor=%23EA4AAA&amp;label=Sponsor&amp;color=2a313c" alt="GH Sponsors badge" /></a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7245906</code></a> Merge pull request <a href="">#427</a> from sethmlarson/certifi-sigstore</li>
<li><a href=""><code>331eccb</code></a> Upgrade certifi and sigstore</li>
<li><a href=""><code>f68fee4</code></a> 💰 Sync the FUNDING config</li>
<li><a href=""><code>c0d6f8e</code></a> Merge branch 'integrity/runtime/deptree' into unstable/v1</li>
<li><a href=""><code>9090099</code></a> 🧪 Make smoke test deps hash-pinned in CI</li>
<li><a href=""><code>34e40c2</code></a> 📌 Bump pip-tools managed transitive deptrees</li>
<li><a href=""><code>e800ed5</code></a> 👷 Enable hash-checking in the runtime deptree 🔗</li>
<li><a href=""><code>dd8c5f4</code></a> 🔧 Make pip-tools config available in container</li>
<li>See full diff in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/dc37677b2e1c63e2034f94d8a5b11f265b73ba33...7245906fb61fa33a13554f9d5fb856fe61758086">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pypa/gh-action-pypi-publish&package-manager=github_actions&previous-version=1.14.2&new-version=1.14.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31f074d46988`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
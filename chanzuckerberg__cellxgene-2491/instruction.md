# Issue

**Title:** chore(deps): bump axios from 0.21.1 to 0.21.4 in /client

## Description

Bumps [axios](https://github.com/axios/axios) from 0.21.1 to 0.21.4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/axios/axios/releases">axios's releases</a>.</em></p>
<blockquote>
<h2>v0.21.4</h2>
<h3>0.21.4 (September 6, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Fixing JSON transform when data is stringified. Providing backward compatibility and complying to the JSON RFC standard (<a href="https://github-redirect.dependabot.com/axios/axios/pull/4020">#4020</a>)</li>
</ul>
<p>Huge thanks to everyone who contributed to this release via code (authors listed below) or via reviews and triaging on GitHub:</p>
<ul>
<li><a href="https://github.com/gfortaine">Guillaume Fortaine</a></li>
<li><a href="https://github.com/kawanet">Yusuke Kawasaki</a></li>
<li><a href="https://github.com/DigitalBrainJS">Dmitriy Mozgovoy</a></li>
</ul>
<h2>v0.21.3</h2>
<h3>0.21.3 (September 4, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Fixing response interceptor not being called when request interceptor is attached (<a href="https://github-redirect.dependabot.com/axios/axios/pull/4013">#4013</a>)</li>
</ul>
<p>Huge thanks to everyone who contributed to this release via code (authors listed below) or via reviews and triaging on GitHub:</p>
<ul>
<li><a href="https://github.com/nerdbeere">Julian Hollmann</a></li>
</ul>
<h2>v0.21.2</h2>
<h3>0.21.2 (September 4, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Updating axios requests to be delayed by pre-emptive promise creation (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2702">#2702</a>)</li>
<li>Adding &quot;synchronous&quot; and &quot;runWhen&quot; options to interceptors api (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2702">#2702</a>)</li>
<li>Updating of transformResponse (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3377">#3377</a>)</li>
<li>Adding ability to omit User-Agent header (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3703">#3703</a>)</li>
<li>Adding multiple JSON improvements (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3688">#3688</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3763">#3763</a>)</li>
<li>Fixing quadratic runtime and extra memory usage when setting a maxContentLength (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3738">#3738</a>)</li>
<li>Adding parseInt to config.timeout (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3781">#3781</a>)</li>
<li>Adding custom return type support to interceptor (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3783">#3783</a>)</li>
<li>Adding security fix for ReDoS vulnerability (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3980">#3980</a>)</li>
</ul>
<p>Internal and Tests:</p>
<ul>
<li>Updating build dev dependancies (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3401">#3401</a>)</li>
<li>Fixing builds running on Travis CI (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3538">#3538</a>)</li>
<li>Updating follow rediect version (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3694">#3694</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3771">#3771</a>)</li>
<li>Updating karma sauce launcher to fix failing sauce tests (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3712">#3712</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3717">#3717</a>)</li>
<li>Updating content-type header for application/json to not contain charset field, according do RFC 8259 (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2154">#2154</a>)</li>
<li>Fixing tests by bumping karma-sauce-launcher version (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3813">#3813</a>)</li>
<li>Changing testing process from Travis CI to GitHub Actions (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3938">#3938</a>)</li>
</ul>
<p>Documentation:</p>
<ul>
<li>Updating documentation around the use of <code>AUTH_TOKEN</code> with multiple domain endpoints (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3539">#3539</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/axios/axios/blob/master/CHANGELOG.md">axios's changelog</a>.</em></p>
<blockquote>
<h3>0.21.4 (September 6, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Fixing JSON transform when data is stringified. Providing backward compatability and complying to the JSON RFC standard (<a href="https://github-redirect.dependabot.com/axios/axios/pull/4020">#4020</a>)</li>
</ul>
<p>Huge thanks to everyone who contributed to this release via code (authors listed below) or via reviews and triaging on GitHub:</p>
<ul>
<li><a href="https://github.com/axios/axios/blob/master/mailto:jasonsaayman@gmail.com">Jay</a></li>
<li><a href="https://github.com/gfortaine">Guillaume Fortaine</a></li>
<li><a href="https://github.com/kawanet">Yusuke Kawasaki</a></li>
<li><a href="https://github.com/DigitalBrainJS">Dmitriy Mozgovoy</a></li>
</ul>
<h3>0.21.3 (September 4, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Fixing response interceptor not being called when request interceptor is attached (<a href="https://github-redirect.dependabot.com/axios/axios/pull/4013">#4013</a>)</li>
</ul>
<p>Huge thanks to everyone who contributed to this release via code (authors listed below) or via reviews and triaging on GitHub:</p>
<ul>
<li><a href="https://github.com/axios/axios/blob/master/mailto:jasonsaayman@gmail.com">Jay</a></li>
<li><a href="https://github.com/nerdbeere">Julian Hollmann</a></li>
</ul>
<h3>0.21.2 (September 4, 2021)</h3>
<p>Fixes and Functionality:</p>
<ul>
<li>Updating axios requests to be delayed by pre-emptive promise creation (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2702">#2702</a>)</li>
<li>Adding &quot;synchronous&quot; and &quot;runWhen&quot; options to interceptors api (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2702">#2702</a>)</li>
<li>Updating of transformResponse (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3377">#3377</a>)</li>
<li>Adding ability to omit User-Agent header (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3703">#3703</a>)</li>
<li>Adding multiple JSON improvements (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3688">#3688</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3763">#3763</a>)</li>
<li>Fixing quadratic runtime and extra memory usage when setting a maxContentLength (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3738">#3738</a>)</li>
<li>Adding parseInt to config.timeout (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3781">#3781</a>)</li>
<li>Adding custom return type support to interceptor (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3783">#3783</a>)</li>
<li>Adding security fix for ReDoS vulnerability (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3980">#3980</a>)</li>
</ul>
<p>Internal and Tests:</p>
<ul>
<li>Updating build dev dependancies (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3401">#3401</a>)</li>
<li>Fixing builds running on Travis CI (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3538">#3538</a>)</li>
<li>Updating follow rediect version (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3694">#3694</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3771">#3771</a>)</li>
<li>Updating karma sauce launcher to fix failing sauce tests (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3712">#3712</a>, <a href="https://github-redirect.dependabot.com/axios/axios/pull/3717">#3717</a>)</li>
<li>Updating content-type header for application/json to not contain charset field, according do RFC 8259 (<a href="https://github-redirect.dependabot.com/axios/axios/pull/2154">#2154</a>)</li>
<li>Fixing tests by bumping karma-sauce-launcher version (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3813">#3813</a>)</li>
<li>Changing testing process from Travis CI to GitHub Actions (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3938">#3938</a>)</li>
</ul>
<p>Documentation:</p>
<ul>
<li>Updating documentation around the use of <code>AUTH_TOKEN</code> with multiple domain endpoints (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3539">#3539</a>)</li>
<li>Remove duplication of item in changelog (<a href="https://github-redirect.dependabot.com/axios/axios/pull/3523">#3523</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>66c4602</code></a> Merge branch 'master' into release/0.21.4</li>
<li><a href=""><code>fc15665</code></a> [Releasing] v0.21.4</li>
<li><a href=""><code>c2714f0</code></a> [Updating] incorrect JSON syntax in README.md</li>
<li><a href=""><code>0fc7248</code></a> fix json transform when data is pre-stringified (<a href="https://github-redirect.dependabot.com/axios/axios/issues/4020">#4020</a>)</li>
<li><a href=""><code>90205f8</code></a> Change headers type to string record (<a href="https://github-redirect.dependabot.com/axios/axios/issues/3021">#3021</a>)</li>
<li><a href=""><code>92b29d2</code></a> Make the default type of response data never (<a href="https://github-redirect.dependabot.com/axios/axios/issues/3002">#3002</a>)</li>
<li><a href=""><code>4eeb3b1</code></a> Improved type-safety for AxiosRequestConfig (<a href="https://github-redirect.dependabot.com/axios/axios/issues/2995">#2995</a>)</li>
<li><a href=""><code>cd7ff04</code></a> Adding HTTP status code to error.toJSON (<a href="https://github-redirect.dependabot.com/axios/axios/issues/2956">#2956</a>)</li>
<li><a href=""><code>b5a1a67</code></a> Adding nodejs http.request option: insecureHTTPParser (<a href="https://github-redirect.dependabot.com/axios/axios/issues/2930">#2930</a>)</li>
<li><a href=""><code>4f25380</code></a> Exposing the Axios constructor in index.d.ts (<a href="https://github-redirect.dependabot.com/axios/axios/issues/2872">#2872</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/axios/axios/compare/v0.21.1...v0.21.4">compare view</a></li>
</ul>
</details>
<details>
<summary>Maintainer changes</summary>
<p>This version was pushed to npm by <a href="https://www.npmjs.com/~jasonsaayman">jasonsaayman</a>, a new releaser for axios since your current version.</p>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=axios&package-manager=npm_and_yarn&previous-version=0.21.1&new-version=0.21.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69a5d5e837a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
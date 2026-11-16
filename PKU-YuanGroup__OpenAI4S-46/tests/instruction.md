# Issue

**Title:** chore(deps): bump https://github.com/pycqa/isort from 5.12.0 to 8.0.1

## Description

Bumps [https://github.com/pycqa/isort](https://github.com/pycqa/isort) from 5.12.0 to 8.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pycqa/isort/releases">https://github.com/pycqa/isort's releases</a>.</em></p>
<blockquote>
<h2>8.0.1</h2>
<h2>Changes</h2>
<ul>
<li>Fix <a href="">#2461</a>: Added compression to stdlibs for Python 3.14 in isort/stdlibs/py314.py (<a href="">#2463</a>) <a href="https://github.com/FinlayTheBerry"><code>@​FinlayTheBerry</code></a></li>
<li>Fix unindented comments being corrupted in indented blocks (<a href="">#2459</a>) <a href="https://github.com/worksbyfriday"><code>@​worksbyfriday</code></a></li>
</ul>
<h2>8.0.0</h2>
<h2>Changes</h2>
<ul>
<li>Update CHANGELOG for version 8.0.0 (<a href="">#2460</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>Fix edge case of <code>__future__</code> import. (<a href="">#2458</a>) <a href="https://github.com/skv0zsneg"><code>@​skv0zsneg</code></a></li>
<li>Fix the Plone profile to be compatible with black (<a href="">#2457</a>) <a href="https://github.com/ale-rt"><code>@​ale-rt</code></a></li>
<li>typo fix (<a href="">#2450</a>) <a href="https://github.com/jsta"><code>@​jsta</code></a></li>
<li>Remove the <code>setuptools</code> plugin (<a href="">#2427</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>Turn some warnings into errors in test suite (<a href="">#2449</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>chore: replace black with ruff in clean.sh (<a href="">#2448</a>) <a href="https://github.com/joao-faria-dev"><code>@​joao-faria-dev</code></a></li>
<li>feat!: remove old finders flag and legacy finder logic (<a href="">#2446</a>) <a href="https://github.com/joao-faria-dev"><code>@​joao-faria-dev</code></a></li>
<li>Fix whitespace insensitive check triggering on tabs (<a href="">#2437</a>) <a href="https://github.com/robsdedude"><code>@​robsdedude</code></a></li>
<li>Fix line separator detection not considering form feed as white space (<a href="">#2436</a>) <a href="https://github.com/robsdedude"><code>@​robsdedude</code></a></li>
<li>Fix <a href="">#1964</a>: <code>lines_before_import</code> sometimes ignored (<a href="">#1965</a>) <a href="https://github.com/robsdedude"><code>@​robsdedude</code></a></li>
<li>Remove reference to 3.9 in README (<a href="">#2434</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
</ul>
<h2>:rocket: Features</h2>
<ul>
<li>Ensure <code>multiprocessing.Pool</code> is always closed and joined (<a href="">#2442</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
</ul>
<h2>:construction_worker: Continuous Integration</h2>
<ul>
<li>Simplify CI by putting similar steps into a single action file (<a href="">#2444</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
</ul>
<h2>:package: Dependencies</h2>
<ul>
<li>Bump actions/checkout from 5 to 6 in the github-actions group (<a href="">#2451</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump astral-sh/setup-uv from 6 to 7 in the github-actions group (<a href="">#2441</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
</ul>
<h2>7.0.0</h2>
<h2>Changes</h2>
<h2>:boom: Breaking Changes</h2>
<ul>
<li>Drop support for Python 3.9 (<a href="">#2430</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
</ul>
<h2>:rocket: Features</h2>
<ul>
<li>Show absolute paths in skipped file messages (<a href="">#2416</a>) <a href="https://github.com/pranlawate"><code>@​pranlawate</code></a></li>
</ul>
<h2>:beetle: Fixes</h2>
<ul>
<li>Some fixes for Python 3.14 (<a href="">#2433</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>Test on <code>3.14</code> and fix any bugs (<a href="">#2425</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/PyCQA/isort/blob/main/CHANGELOG.md">https://github.com/pycqa/isort's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<p>NOTE: isort follows the <a href="https://semver.org/">semver</a> versioning standard.
Find out more about isort's release policy <a href="https://github.com/PyCQA/isort/blob/main/docs/major_releases/release_policy.md">here</a>.</p>
<h2>Releases</h2>
<h3>Unreleased</h3>
<h3>8.0.0 February 19 2026</h3>
<ul>
<li>Removed <code>--old-finders</code> and <code>--magic-placement</code> flags and <code>old_finders</code> configuration option. The legacy finder logic that relied on environment introspection has been removed (<a href="">#2445</a>) <a href="https://github.com/joao-faria-dev"><code>@​joao-faria-dev</code></a></li>
<li>Update the <code>plone</code> profile to not clash with <code>black</code> (<a href="">#2456</a>) <a href="https://github.com/ale-rt"><code>@​ale-rt</code></a></li>
</ul>
<h3>6.1.0 October 1 2025</h3>
<ul>
<li>Add python 3.14 classifier and badge (<a href="">#2409</a>) <a href="https://github.com/staticdev"><code>@​staticdev</code></a></li>
<li>Drop use of non-standard pkg_resources API (<a href="">#2405</a>) <a href="https://github.com/dvarrazzo"><code>@​dvarrazzo</code></a></li>
</ul>
<h3>6.0.1 Febuary 26 2025</h3>
<ul>
<li>Add OSError handling in find_imports_in_file (<a href="">#2331</a>) <a href="https://github.com/kobarity"><code>@​kobarity</code></a></li>
</ul>
<h3>6.0.0 January 27 2025</h3>
<ul>
<li>Remove support for Python 3.8 (<a href="">#2327</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>Python 3.13 support (<a href="">#2306</a>) <a href="https://github.com/mayty"><code>@​mayty</code></a></li>
<li>Speed up exists_case_sensitive calls (<a href="">#2264</a>) <a href="https://github.com/correctmost"><code>@​correctmost</code></a></li>
<li>Ensure that split_on_trailing_comma works with as imports (<a href="">#2340</a>) <a href="https://github.com/DanielNoord"><code>@​DanielNoord</code></a></li>
<li>Black profile: enable magic comma (<a href="">#2236</a>) <a href="https://github.com/MrMino"><code>@​MrMino</code></a></li>
<li>Update line_length and single_line_exclusions in google profile (<a href="">#2149</a>) <a href="https://github.com/jagapiou"><code>@​jagapiou</code></a></li>
<li>Allow --diff to be used with --jobs (<a href="">#2302</a>) <a href="https://github.com/mnakama"><code>@​mnakama</code></a></li>
<li>Fix wemake profile to have correct character limit (<a href="">#2241</a>) <a href="https://github.com/sobolevn"><code>@​sobolevn</code></a></li>
<li>Fix sort_reexports code mangling (<a href="">#2283</a>) <a href="https://github.com/Helveg"><code>@​Helveg</code></a></li>
<li>Fix correct group by package tokenization (<a href="">#2136</a>) <a href="https://github.com/glasnt"><code>@​glasnt</code></a></li>
</ul>
<h3>5.13.2 December 13 2023</h3>
<ul>
<li>Apply the bracket fix from issue <a href="">#471</a> only for use_parentheses=True (<a href="">#2184</a>) <a href="https://github.com/bp72"><code>@​bp72</code></a></li>
<li>Confine pre-commit to stages (<a href="">#2213</a>) <a href="https://github.com/davidculley"><code>@​davidculley</code></a></li>
<li>Fixed colors extras (<a href="">#2212</a>) <a href="https://github.com/staticdev"><code>@​staticdev</code></a></li>
</ul>
<h3>5.13.1 December 11 2023</h3>
<ul>
<li>Fixed integration tests (<a href="">#2208</a>) <a href="https://github.com/bp72"><code>@​bp72</code></a></li>
<li>Fixed normalizing imports from more than one level of parent modules (issue/2152) (<a href="">#2191</a>) <a href="https://github.com/bp72"><code>@​bp72</code></a></li>
<li>Remove optional dependencies without extras (<a href="">#2207</a>) <a href="https://github.com/staticdev"><code>@​staticdev</code></a></li>
</ul>
<h3>5.13.0 December 9 2023</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a333737</code></a> Merge pull request <a href="">#2463</a> from FinlayTheBerry/issue/2461</li>
<li><a href=""><code>878ba7e</code></a> Added compression to stdlibs for Python 3.14 in isort/stdlibs/py314.py</li>
<li><a href=""><code>b5f06a7</code></a> Merge pull request <a href="">#2459</a> from Fridayai700/fix-unindented-comment-corruption</li>
<li><a href=""><code>3459bde</code></a> Merge pull request <a href="">#2460</a> from PyCQA/DanielNoord-patch-1</li>
<li><a href=""><code>6e70bb6</code></a> Update CHANGELOG for version 8.0.0</li>
<li><a href=""><code>fd2514b</code></a> Fix unindented comments being corrupted in indented blocks</li>
<li><a href=""><code>b0f2dab</code></a> Merge pull request <a href="">#2458</a> from skv0zsneg/issue/1882</li>
<li><a href=""><code>313797b</code></a> Fix lint.</li>
<li><a href=""><code>7d3a6f5</code></a> Add ignore for cyclomatic complexity check.</li>
<li><a href=""><code>6b9f895</code></a> Remove debug prints.</li>
<li>Additional commits viewable in <a href="https://github.com/pycqa/isort/compare/5.12.0...8.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=https://github.com/pycqa/isort&package-manager=pre_commit&previous-version=5.12.0&new-version=8.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c046f7338c5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
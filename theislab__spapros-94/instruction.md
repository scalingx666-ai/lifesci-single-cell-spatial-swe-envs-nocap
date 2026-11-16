# Issue

**Title:** [DEPENDABOT]: Bump jinja2 from 2.11.3 to 3.0.1

## Description

Bumps [jinja2](https://github.com/pallets/jinja) from 2.11.3 to 3.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pallets/jinja/releases">jinja2's releases</a>.</em></p>
<blockquote>
<h2>3.0.1</h2>
<ul>
<li>Changes: <a href="https://jinja.palletsprojects.com/en/3.0.x/changes/#version-3-0-1">https://jinja.palletsprojects.com/en/3.0.x/changes/#version-3-0-1</a></li>
</ul>
<h2>3.0.0</h2>
<p>New major versions of all the core Pallets libraries, including Jinja 3.0, have been released! :tada:</p>
<ul>
<li>Read the announcement on our blog: <a href="https://palletsprojects.com/blog/flask-2-0-released/">https://palletsprojects.com/blog/flask-2-0-released/</a></li>
<li>Read the full list of changes: <a href="https://jinja.palletsprojects.com/changes/#version-3-0-0">https://jinja.palletsprojects.com/changes/#version-3-0-0</a></li>
<li>Retweet the announcement on Twitter: <a href="https://twitter.com/PalletsTeam/status/1392266507296514048">https://twitter.com/PalletsTeam/status/1392266507296514048</a></li>
<li>Follow our blog, Twitter, or GitHub to see future announcements.</li>
</ul>
<p>This represents a significant amount of work, and there are quite a few changes. Be sure to carefully read the changelog, and use tools such as pip-compile and Dependabot to pin your dependencies and control your updates.</p>
<h2>3.0.0rc2</h2>
<p>Fixes an issue with the deprecated <code>Markup</code> subclass, <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1401">#1401</a>.</p>
<ul>
<li>Changes: <a href="https://jinja.palletsprojects.com/en/master/changes/#version-3-0-0">https://jinja.palletsprojects.com/en/master/changes/#version-3-0-0</a></li>
</ul>
<h2>3.0.0rc1</h2>
<ul>
<li>Changes: <a href="https://jinja.palletsprojects.com/en/master/changes/#version-3-0-0">https://jinja.palletsprojects.com/en/master/changes/#version-3-0-0</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pallets/jinja/blob/main/CHANGES.rst">jinja2's changelog</a>.</em></p>
<blockquote>
<h2>Version 3.0.1</h2>
<p>Released 2021-05-18</p>
<ul>
<li>Update MarkupSafe dependency to &gt;= 2.0. :pr:<code>1418</code></li>
<li>Mark top-level names as exported so type checking understands
imports in user projects. :issue:<code>1426</code></li>
<li>Fix some types that weren't available in Python 3.6.0. :issue:<code>1433</code></li>
<li>The deprecation warning for unneeded <code>autoescape</code> and <code>with_</code>
extensions shows more relevant context. :issue:<code>1429</code></li>
<li>Fixed calling deprecated <code>jinja2.Markup</code> without an argument.
Use <code>markupsafe.Markup</code> instead. :issue:<code>1438</code></li>
<li>Calling sync <code>render</code> for an async template uses <code>asyncio.run</code>
on Python &gt;= 3.7. This fixes a deprecation that Python 3.10
introduces. :issue:<code>1443</code></li>
</ul>
<h2>Version 3.0.0</h2>
<p>Released 2021-05-11</p>
<ul>
<li>Drop support for Python 2.7 and 3.5.</li>
<li>Bump MarkupSafe dependency to &gt;=1.1.</li>
<li>Bump Babel optional dependency to &gt;=2.1.</li>
<li>Remove code that was marked deprecated.</li>
<li>Add type hinting. :pr:<code>1412</code></li>
<li>Use :pep:<code>451</code> API to load templates with
:class:<code>~loaders.PackageLoader</code>. :issue:<code>1168</code></li>
<li>Fix a bug that caused imported macros to not have access to the
current template's globals. :issue:<code>688</code></li>
<li>Add ability to ignore <code>trim_blocks</code> using <code>+%}</code>. :issue:<code>1036</code></li>
<li>Fix a bug that caused custom async-only filters to fail with
constant input. :issue:<code>1279</code></li>
<li>Fix UndefinedError incorrectly being thrown on an undefined variable
instead of <code>Undefined</code> being returned on
<code>NativeEnvironment</code> on Python 3.10. :issue:<code>1335</code></li>
<li>Blocks can be marked as <code>required</code>. They must be overridden at
some point, but not necessarily by the direct child. :issue:<code>1147</code></li>
<li>Deprecate the <code>autoescape</code> and <code>with</code> extensions, they are
built-in to the compiler. :issue:<code>1203</code></li>
<li>The <code>urlize</code> filter recognizes <code>mailto:</code> links and takes
<code>extra_schemes</code> (or <code>env.policies[&quot;urlize.extra_schemes&quot;]</code>) to
recognize other schemes. It tries to balance parentheses within a
URL instead of ignoring trailing characters. The parsing in general
has been updated to be more efficient and match more cases. URLs
without a scheme are linked as <code>https://</code> instead of <code>http://</code>.
:issue:<code>522, 827, 1172</code>, :pr:<code>1195</code></li>
<li>Filters that get attributes, such as <code>map</code> and <code>groupby</code>, can</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3b3e16f</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1445">#1445</a> from pallets/release-3.0.1</li>
<li><a href=""><code>4d23bfb</code></a> release version 3.0.1</li>
<li><a href=""><code>77674b9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1444">#1444</a> from pallets/event-loop</li>
<li><a href=""><code>7d0b7ac</code></a> use asyncio.run</li>
<li><a href=""><code>94a6423</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1442">#1442</a> from dannysepler/use-pathlib-in-places</li>
<li><a href=""><code>06c646d</code></a> Use pathlib in some test places</li>
<li><a href=""><code>9f5db9a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1440">#1440</a> from pallets/deprecated-markup</li>
<li><a href=""><code>f562a4f</code></a> fix deprecated <code>Markup</code> subclass</li>
<li><a href=""><code>fb564a8</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/jinja/issues/1436">#1436</a> from pallets/deprecated-extensions</li>
<li><a href=""><code>b4d31e7</code></a> show context for deprecated extensions</li>
<li>Additional commits viewable in <a href="https://github.com/pallets/jinja/compare/2.11.3...3.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=jinja2&package-manager=pip&previous-version=2.11.3&new-version=3.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10460ca399e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
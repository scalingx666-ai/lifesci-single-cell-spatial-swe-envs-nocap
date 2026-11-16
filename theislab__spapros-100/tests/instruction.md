# Issue

**Title:** [DEPENDABOT]: Bump click from 7.1.2 to 8.0.1

## Description

Bumps [click](https://github.com/pallets/click) from 7.1.2 to 8.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pallets/click/releases">click's releases</a>.</em></p>
<blockquote>
<h2>8.0.1</h2>
<ul>
<li>Changes: <a href="https://click.palletsprojects.com/en/8.0.x/changes/#version-8-0-1">https://click.palletsprojects.com/en/8.0.x/changes/#version-8-0-1</a></li>
</ul>
<h2>8.0.0</h2>
<p>New major versions of all the core Pallets libraries, including Click 8.0, have been released! :tada:</p>
<ul>
<li>Read the announcement on our blog: <a href="https://palletsprojects.com/blog/flask-2-0-released/">https://palletsprojects.com/blog/flask-2-0-released/</a></li>
<li>Read the full list of changes: <a href="https://click.palletsprojects.com/changes/#version-8-0-0">https://click.palletsprojects.com/changes/#version-8-0-0</a></li>
<li>Retweet the announcement on Twitter: <a href="https://twitter.com/PalletsTeam/status/1392266507296514048">https://twitter.com/PalletsTeam/status/1392266507296514048</a></li>
<li>Follow our blog, Twitter, or GitHub to see future announcements.</li>
</ul>
<p>This represents a significant amount of work, and there are quite a few changes. Be sure to carefully read the changelog, and use tools such as pip-compile and Dependabot to pin your dependencies and control your updates.</p>
<h2>8.0.0rc1</h2>
<ul>
<li>Changes: <a href="https://click.palletsprojects.com/en/master/changes/#version-8-0">https://click.palletsprojects.com/en/master/changes/#version-8-0</a></li>
</ul>
<h2>8.0.0a1</h2>
<ul>
<li>Changes: <a href="https://click.palletsprojects.com/en/master/changelog/#version-8-0">https://click.palletsprojects.com/en/master/changelog/#version-8-0</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pallets/click/blob/main/CHANGES.rst">click's changelog</a>.</em></p>
<blockquote>
<h2>Version 8.0.1</h2>
<p>Released 2021-05-19</p>
<ul>
<li>Mark top-level names as exported so type checking understand imports
in user projects. :issue:<code>1879</code></li>
<li>Annotate <code>Context.obj</code> as <code>Any</code> so type checking allows all
operations on the arbitrary object. :issue:<code>1885</code></li>
<li>Fix some types that weren't available in Python 3.6.0. :issue:<code>1882</code></li>
<li>Fix type checking for iterating over <code>ProgressBar</code> object.
:issue:<code>1892</code></li>
<li>The <code>importlib_metadata</code> backport package is installed on Python &lt;
3.8. :issue:<code>1889</code></li>
<li>Arguments with <code>nargs=-1</code> only use env var value if no command
line values are given. :issue:<code>1903</code></li>
<li>Flag options guess their type from <code>flag_value</code> if given, like
regular options do from <code>default</code>. :issue:<code>1886</code></li>
<li>Added documentation that custom parameter types may be passed
already valid values in addition to strings. :issue:<code>1898</code></li>
<li>Resolving commands returns the name that was given, not
<code>command.name</code>, fixing an unintended change to help text and
<code>default_map</code> lookups. When using patterns like <code>AliasedGroup</code>,
override <code>resolve_command</code> to change the name that is returned if
needed. :issue:<code>1895</code></li>
<li>If a default value is invalid, it does not prevent showing help
text. :issue:<code>1889</code></li>
<li>Pass <code>windows_expand_args=False</code> when calling the main command to
disable pattern expansion on Windows. There is no way to escape
patterns in CMD, so if the program needs to pass them on as-is then
expansion must be disabled. :issue:<code>1901</code></li>
</ul>
<h2>Version 8.0.0</h2>
<p>Released 2021-05-11</p>
<ul>
<li>Drop support for Python 2 and 3.5.</li>
<li>Colorama is always installed on Windows in order to provide style
and color support. :pr:<code>1784</code></li>
<li>Adds a repr to Command, showing the command name for friendlier
debugging. :issue:<code>1267</code>, :pr:<code>1295</code></li>
<li>Add support for distinguishing the source of a command line
parameter. :issue:<code>1264</code>, :pr:<code>1329</code></li>
<li>Add an optional parameter to <code>ProgressBar.update</code> to set the
<code>current_item</code>. :issue:<code>1226</code>, :pr:<code>1332</code></li>
<li><code>version_option</code> uses <code>importlib.metadata</code> (or the
<code>importlib_metadata</code> backport) instead of <code>pkg_resources</code>. The
version is detected based on the package name, not the entry point</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>baea623</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/click/issues/1919">#1919</a> from pallets/release-8.0.1</li>
<li><a href=""><code>3149679</code></a> release version 8.0.1</li>
<li><a href=""><code>6e91b13</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/click/issues/1918">#1918</a> from pallets/disable-windows-expansion</li>
<li><a href=""><code>6439aae</code></a> flag to control Windows pattern expansion</li>
<li><a href=""><code>fcf8205</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/click/issues/1916">#1916</a> from pallets/default-resilient</li>
<li><a href=""><code>985ca16</code></a> show help text with invalid default</li>
<li><a href=""><code>1b49159</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/click/issues/1915">#1915</a> from pallets/command-name</li>
<li><a href=""><code>0db91e2</code></a> return resolved name, not original name</li>
<li><a href=""><code>329b100</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pallets/click/issues/1914">#1914</a> from pallets/custom-type-value</li>
<li><a href=""><code>0c108f2</code></a> document values passed to types</li>
<li>Additional commits viewable in <a href="https://github.com/pallets/click/compare/7.1.2...8.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=click&package-manager=pip&previous-version=7.1.2&new-version=8.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `903cfd516796`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
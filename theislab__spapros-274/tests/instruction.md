# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 4.5.0 to 5.3.0

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 4.5.0 to 5.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/releases">sphinx's releases</a>.</em></p>
<blockquote>
<h2>v5.3.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.2.3</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.2.2</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.2.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.2.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.1.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.1.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.0.2</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.0.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v5.0.0</h2>
<p>No release notes provided.</p>
<h2>v5.0.0b1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/master/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 5.3.0 (released Oct 16, 2022)</h1>
<ul>
<li><a href="">#10759</a>: LaTeX: add :confval:<code>latex_table_style</code> and support the
<code>'booktabs'</code>, <code>'borderless'</code>, and <code>'colorrows'</code> styles.
(thanks to Stefan Wiehler for initial pull requests <a href="">#6666</a>, <a href="">#6671</a>)</li>
<li><a href="">#10840</a>: One can cross-reference including an option value like <code>:option:`--module=foobar```, </code>:option:<code>--module[=foobar]``` or ``:option:</code>--module foobar```.
Patch by Martin Liska.</li>
<li><a href="">#10881</a>: autosectionlabel: Record the generated section label to the debug log.</li>
<li><a href="">#10268</a>: Correctly URI-escape image filenames.</li>
<li><a href="">#10887</a>: domains: Allow sections in all the content of all object description
directives (e.g. :rst:dir:<code>py:function</code>). Patch by Adam Turner</li>
</ul>
<h1>Release 5.2.3 (released Sep 30, 2022)</h1>
<ul>
<li><a href="">#10878</a>: Fix base64 image embedding in <code>sphinx.ext.imgmath</code></li>
<li><a href="">#10886</a>: Add <code>:nocontentsentry:</code> flag and global domain table of contents
entry control option. Patch by Adam Turner</li>
</ul>
<h1>Release 5.2.2 (released Sep 27, 2022)</h1>
<ul>
<li><a href="">#10872</a>: Restore link targets for autodoc modules to the top of content.
Patch by Dominic Davis-Foster.</li>
</ul>
<h1>Release 5.2.1 (released Sep 25, 2022)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#10861</a>: Always normalise the <code>pycon3</code> lexer to <code>pycon</code>.</li>
<li>Fix using <code>sphinx.ext.autosummary</code> with modules containing titles in the
module-level docstring.</li>
</ul>
<h1>Release 5.2.0.post0 (released Sep 24, 2022)</h1>
<ul>
<li>Recreated source tarballs for Debian maintainers.</li>
</ul>
<h1>Release 5.2.0 (released Sep 24, 2022)</h1>
<h2>Dependencies</h2>
<ul>
<li><a href="">#10356</a>: Sphinx now uses declarative metadata with <code>pyproject.toml</code> to
create packages, using PyPA's <code>flit</code> project as a build backend. Patch by</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c1f2a52</code></a> Bump to 5.3.0 final</li>
<li><a href=""><code>10db540</code></a> Allow sections in object description directives (<a href="">#10919</a>)</li>
<li><a href=""><code>0fd4539</code></a> Simplify bug report template</li>
<li><a href=""><code>b58eb61</code></a> Update all GitHub actions workflows to Ubuntu latest</li>
<li><a href=""><code>3e04952</code></a> Add <code>sphinx-build --bug-report</code></li>
<li><a href=""><code>fa6d425</code></a> URI-escape image filenames (<a href="">#10268</a>)</li>
<li><a href=""><code>e008e16</code></a> Revert &quot;Fix detection for out of date files (<a href="">#9360</a>)&quot; (<a href="">#10908</a>)</li>
<li><a href=""><code>cef1a03</code></a> Update image for LaTeX job (<a href="">#10916</a>)</li>
<li><a href=""><code>b5ba1ed</code></a> s/5.2.0/5.3.0 in various code comments as <a href="">#10759</a> got merged in 5.3.0</li>
<li><a href=""><code>3deb527</code></a> Update CHANGES for PR <a href="">#10759</a></li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v4.5.0...v5.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=4.5.0&new-version=5.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91f69685d918`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
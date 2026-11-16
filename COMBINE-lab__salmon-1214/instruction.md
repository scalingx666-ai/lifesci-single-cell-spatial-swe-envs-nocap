# Issue

**Title:** chore(deps): bump zstd from 0.13.3 to 0.14.0

## Description

Bumps [zstd](https://github.com/gyscos/zstd-rs) from 0.13.3 to 0.14.0.
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>648acb4</code></a> Avoid let...else in the seekable callbacks</li>
<li><a href=""><code>e1152c1</code></a> Bump versions for the next release</li>
<li><a href=""><code>7caed6e</code></a> Derive the usual traits on ResetDirective</li>
<li><a href=""><code>bf7b1f7</code></a> Refuse to reuse a context an error may have left undefined</li>
<li><a href=""><code>1565618</code></a> Check the target, not the host, for MSVC</li>
<li><a href=""><code>8315a62</code></a> Return Ok(0) from Read::read for an empty buffer</li>
<li><a href=""><code>a7cfa93</code></a> Keep the std gate on the Cursor WriteBuf impl</li>
<li><a href=""><code>9bf1692</code></a> Say why the Send and Sync impls hold</li>
<li><a href=""><code>681bcc3</code></a> Don't truncate Cursor positions on 32-bit targets</li>
<li><a href=""><code>d5a1fdd</code></a> Don't hand out a &amp;mut Seekable from AdvancedSeekable</li>
<li>Additional commits viewable in <a href="https://github.com/gyscos/zstd-rs/compare/v0.13.3...v0.14.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=zstd&package-manager=cargo&previous-version=0.13.3&new-version=0.14.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcea903bb940`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
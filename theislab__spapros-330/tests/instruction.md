# Issue

**Title:** [DEPENDABOT]: Bump pillow from 10.2.0 to 10.3.0

## Description

Bumps [pillow](https://github.com/python-pillow/Pillow) from 10.2.0 to 10.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/python-pillow/Pillow/releases">pillow's releases</a>.</em></p>
<blockquote>
<h2>10.3.0</h2>
<p><a href="https://pillow.readthedocs.io/en/stable/releasenotes/10.3.0.html">https://pillow.readthedocs.io/en/stable/releasenotes/10.3.0.html</a></p>
<h2>Changes</h2>
<ul>
<li>CVE-2024-28219: Use strncpy to avoid buffer overflow <a href="">#7928</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Use <code>functools.lru_cache</code> for <code>hopper()</code> <a href="">#7912</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Raise ValueError if seeking to greater than offset-sized integer in TIFF <a href="">#7883</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Improve speed of loading QOI images <a href="">#7925</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Added RGB to I;16N conversion <a href="">#7920</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Add --report argument to <strong>main</strong>.py to omit supported formats <a href="">#7818</a> [<a href="https://github.com/nulano"><code>@​nulano</code></a>]</li>
<li>Added RGB to I;16, I;16L and I;16B conversion <a href="">#7918</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fix editable installation with custom build backend and configuration options <a href="">#7658</a> [<a href="https://github.com/nulano"><code>@​nulano</code></a>]</li>
<li>Fix putdata() for I;16N on big-endian <a href="">#7209</a> [<a href="https://github.com/Yay295"><code>@​Yay295</code></a>]</li>
<li>Determine MPO size from markers, not EXIF data <a href="">#7884</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Improved conversion from RGB to RGBa, LA and La <a href="">#7888</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Support FITS images with GZIP_1 compression <a href="">#7894</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Use I;16 mode for 9-bit JPEG 2000 images <a href="">#7900</a> [<a href="https://github.com/scaramallion"><code>@​scaramallion</code></a>]</li>
<li>Raise ValueError if kmeans is negative <a href="">#7891</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Remove TIFF tag OSUBFILETYPE when saving using libtiff <a href="">#7893</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Raise ValueError for negative values when loading P1-P3 PPM images <a href="">#7882</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Added reading of JPEG2000 palettes <a href="">#7870</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Added alpha_quality argument when saving WebP images <a href="">#7872</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fixed joined corners for ImageDraw rounded_rectangle() non-integer dimensions <a href="">#7881</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Removed Python and NumPy pinning on Cygwin <a href="">#7880</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Update UnidentifiedImageError and <strong>version</strong> imports <a href="">#7644</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Stop reading EPS image at EOF marker <a href="">#7753</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>PSD layer co-ordinates may be negative <a href="">#7706</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Use subprocess with CREATE_NO_WINDOW flag in ImageShow WindowsViewer <a href="">#7791</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>When saving GIF frame that restores to background color, do not fill identical pixels <a href="">#7788</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fixed reading PNG iCCP compression method <a href="">#7823</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Allow writing IFDRational to UNDEFINED tag <a href="">#7840</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fix logged tag name when loading Exif data <a href="">#7842</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Use maximum frame size in IHDR chunk when saving APNG images <a href="">#7821</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Prevent opening P TGA images without a palette <a href="">#7797</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Use palette when loading ICO images <a href="">#7798</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Use consistent arguments for load_read and load_seek <a href="">#7713</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Turn off nullability warnings for macOS SDK <a href="">#7827</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fix shift-sign issue in Convert.c <a href="">#7838</a> [<a href="https://github.com/r-barnes"><code>@​r-barnes</code></a>]</li>
<li>winbuild: Refactor dependency versions into constants <a href="">#7843</a> [<a href="https://github.com/hugovk"><code>@​hugovk</code></a>]</li>
<li>Build macOS arm64 wheels natively <a href="">#7852</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Fixed typo <a href="">#7855</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Open 16-bit grayscale PNGs as I;16 <a href="">#7849</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Handle truncated chunks at the end of PNG images <a href="">#7709</a> [<a href="https://github.com/lajiyuan"><code>@​lajiyuan</code></a>]</li>
<li>Match mask size to pasted image size in GifImagePlugin <a href="">#7779</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Changed SupportsGetMesh protocol to be public <a href="">#7841</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Release GIL while calling <code>WebPAnimDecoderGetNext</code> <a href="">#7782</a> [<a href="https://github.com/evanmiller"><code>@​evanmiller</code></a>]</li>
<li>Fixed reading FLI/FLC images with a prefix chunk <a href="">#7804</a> [<a href="https://github.com/twolife"><code>@​twolife</code></a>]</li>
<li>Updated package name for Tidelift <a href="">#7810</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
<li>Removed unused code <a href="">#7744</a> [<a href="https://github.com/radarhere"><code>@​radarhere</code></a>]</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/python-pillow/Pillow/blob/main/CHANGES.rst">pillow's changelog</a>.</em></p>
<blockquote>
<h2>10.3.0 (2024-04-01)</h2>
<ul>
<li>
<p>CVE-2024-28219: Use <code>strncpy</code> to avoid buffer overflow <a href="">#7928</a>
[radarhere, hugovk]</p>
</li>
<li>
<p>Deprecate <code>eval()</code>, replacing it with <code>lambda_eval()</code> and <code>unsafe_eval()</code> <a href="">#7927</a>
[radarhere, hugovk]</p>
</li>
<li>
<p>Raise <code>ValueError</code> if seeking to greater than offset-sized integer in TIFF <a href="">#7883</a>
[radarhere]</p>
</li>
<li>
<p>Add <code>--report</code> argument to <code>__main__.py</code> to omit supported formats <a href="">#7818</a>
[nulano, radarhere, hugovk]</p>
</li>
<li>
<p>Added RGB to I;16, I;16L, I;16B and I;16N conversion <a href="">#7918</a>, <a href="">#7920</a>
[radarhere]</p>
</li>
<li>
<p>Fix editable installation with custom build backend and configuration options <a href="">#7658</a>
[nulano, radarhere]</p>
</li>
<li>
<p>Fix putdata() for I;16N on big-endian <a href="">#7209</a>
[Yay295, hugovk, radarhere]</p>
</li>
<li>
<p>Determine MPO size from markers, not EXIF data <a href="">#7884</a>
[radarhere]</p>
</li>
<li>
<p>Improved conversion from RGB to RGBa, LA and La <a href="">#7888</a>
[radarhere]</p>
</li>
<li>
<p>Support FITS images with GZIP_1 compression <a href="">#7894</a>
[radarhere]</p>
</li>
<li>
<p>Use I;16 mode for 9-bit JPEG 2000 images <a href="">#7900</a>
[scaramallion, radarhere]</p>
</li>
<li>
<p>Raise ValueError if kmeans is negative <a href="">#7891</a>
[radarhere]</p>
</li>
<li>
<p>Remove TIFF tag OSUBFILETYPE when saving using libtiff <a href="">#7893</a>
[radarhere]</p>
</li>
<li>
<p>Raise ValueError for negative values when loading P1-P3 PPM images <a href="">#7882</a>
[radarhere]</p>
</li>
<li>
<p>Added reading of JPEG2000 palettes <a href="">#7870</a>
[radarhere]</p>
</li>
<li>
<p>Added alpha_quality argument when saving WebP images <a href="">#7872</a>
[radarhere]</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5c89d88</code></a> 10.3.0 version bump</li>
<li><a href=""><code>63cbfcf</code></a> Update CHANGES.rst [ci skip]</li>
<li><a href=""><code>2776126</code></a> Merge pull request <a href="">#7928</a> from python-pillow/lcms</li>
<li><a href=""><code>aeb51cb</code></a> Merge branch 'main' into lcms</li>
<li><a href=""><code>5beb0b6</code></a> Update CHANGES.rst [ci skip]</li>
<li><a href=""><code>cac6ffa</code></a> Merge pull request <a href="">#7927</a> from python-pillow/imagemath</li>
<li><a href=""><code>f5eeeac</code></a> Name as 'options' in lambda_eval and unsafe_eval, but '_dict' in deprecated eval</li>
<li><a href=""><code>facf3af</code></a> Added release notes</li>
<li><a href=""><code>2a93aba</code></a> Use strncpy to avoid buffer overflow</li>
<li><a href=""><code>a670597</code></a> Update CHANGES.rst [ci skip]</li>
<li>Additional commits viewable in <a href="https://github.com/python-pillow/Pillow/compare/10.2.0...10.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pillow&package-manager=pip&previous-version=10.2.0&new-version=10.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47c3ba025c4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
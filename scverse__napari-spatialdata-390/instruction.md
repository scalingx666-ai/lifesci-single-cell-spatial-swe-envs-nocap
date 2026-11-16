# Issue

**Title:** Patch headless tests due to `QT_QPA_PLATFORM=offscreen` edgecase

## Description

# Human notes

This patch only affects tests run within certain compute environments. Solution and description below are from Claude. Patch to be removed once the problems are fixed upstream.

# AI notes
## Fix: image layer tests fail in headless mode (`QT_QPA_PLATFORM=offscreen`)

  ### Problem

  When running on Linux without a display (e.g. CI without Xvfb), `QT_QPA_PLATFORM=offscreen` is set so Qt can initialise without a screen. In this configuration, adding any image layer to a      
  napari viewer crashes with two cascading errors:
                                                                                                                                                                                                    
  1. **`AttributeError: 'NoneType' object has no attribute 'decode'`** — `vispy/gloo/gl/_pyopengl2.py` calls `GL.glGetString(GL_EXTENSIONS).decode('utf-8')` without guarding against `None`, which 
  is what the offscreen GL context returns. This propagates out of `napari._vispy.utils.gl.get_gl_extensions()`.
                                                                                                                                                                                                    
  2. **`TypeError: 'NoneType' object cannot be interpreted as an integer`** — in the same context, `glGetIntegerv(GL_MAX_TEXTURE_SIZE)` returns an empty tuple `()`. Because `()` is falsy, napari's
   `get_max_texture_sizes()` converts it to `None` via `if not max_size_2d: max_size_2d = None`, then passes it as `tile_size` to `TiledImageNode`.
                                                                                                                                                                                                    
  The result: any test that adds an image layer fails, and the leaked `QtViewer` object causes all subsequent tests in the same session to error out in setup.

  ### Fix

  `_patch_napari_gl_for_headless()` is added to `conftest.py` and called when `QT_QPA_PLATFORM=offscreen` is detected. It applies two targeted patches before any test runs:                        
   
  - **`vispy.gloo.gl._pyopengl2.glGetParameter`** — returns `""` instead of crashing when `glGetString` returns `None`, and `0` instead of `()` for empty integer results.                          
  - **`napari._vispy.utils.gl.get_max_texture_sizes`** (and the five napari modules that imported it by name) — falls back to `(2048, 2048)` when the GL query returns a zero/empty value.
                                                                                                                                                                                                    
  Both patches are no-ops in environments that have a real display (CI with Xvfb, macOS, local dev).
                                                                                                                                                                                                    
  ### Temporary workaround                                  

  These are upstream bugs that should be fixed in vispy and napari respectively. The patch and this note should be removed once:                                                                    
  - vispy adds a `None` guard in `_pyopengl2.glGetParameter` for string queries
  - napari catches `AttributeError` in `get_gl_extensions()` and uses a non-zero fallback in `get_max_texture_sizes()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07ff794ac847`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
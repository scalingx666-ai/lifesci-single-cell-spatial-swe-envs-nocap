# Issue

**Title:** Qt6 support: all extra installs napari[qt], fix ROI drawing on PyQt6

## Description

.

napari 0.10 requires Qt >= 6.7 and no longer has a `pyqt5` extra. So `pip install napari-spatialdata[all]` installs no Qt binding at all (pip only warns), and an env with PyQt5 fails at `import napari._qt`. Our CI didn't catch this because `tox.ini` installs `PyQt5` directly.

### Changes
- `setup.cfg`: `all = napari[pyqt5]` becomes `napari[pyqt6]`. That pins the binding napari-spatialdata is tested with, and napari's extra keeps compatible PyQt6/Qt versions. `napari[qt]` would instead follow napari to whatever binding it defaults to next, possibly before this plugin's Qt code (widgets, pyqtgraph) is tested on it. README updated to match.
- `tox.ini`: drop the explicit `PyQt5`. CI now gets Qt from the `all` extra, the same way users do.
- `_scatterwidgets.py` (**user-facing bug on Qt6**): ROI drawing in the scatter widget passed `event.pos()` (`QPoint`) to `mapSceneToView` / `sceneBoundingRect().contains`. PyQt6 no longer converts `QPoint` to `QPointF` implicitly, so every press/move/release while drawing raised `TypeError` and no ROI was created.
  - The handlers now compute the scene position once as `scene_pos = self.mapToScene(event.pos())`, which is a `QPointF` on every binding, and use it throughout. `mouseReleaseEvent` is also called by `scene().sigMouseClicked` with a pyqtgraph `MouseClickEvent` (whose `pos()` `mapToScene` can't take), so its position debug log is now limited to `QMouseEvent`.
  - Before, the viewport position `event.pos()` was used as a scene position, mixed with a `scene_pos` variable holding the same value. That only worked because pyqtgraph's default `autoPixelRange` keeps scene coordinates equal to viewport pixels, so the values don't change.
  - Also fixed a debug log message that was missing its `f` prefix.
- Tests:
  - `test_old_annotation` patched `"PyQt5.QtWidgets.QMessageBox.question"`. It now uses `mocker.patch.object(QtWidgets.QMessageBox, ...)` via qtpy.
  - `send_mouse_event` now passes a `QPointF` to `QMouseEvent`.

### Tested
Tested in a Linux env with napari 0.10.0 + PyQt6 6.12.0 (headless, conftest's `QT_QPA_PLATFORM=offscreen`):
- before: `ImportError` in conftest with PyQt5. With PyQt6 but without the code changes: 3 failed (`test_old_annotation`, `test_roi_from_mouse_events`, `test_remove_roi_double_click`).
- after, napari 0.10.0 + PyQt6: **87 passed**, 12 skipped, 3 xfailed.
- after, napari 0.9.2 + PyQt5 5.15 (`QT_API=pyqt5`): **87 passed**, so nothing changes on the old binding.
- `pip install --dry-run -e ".[all]"` resolves napari 0.10.0 + PyQt6 6.12.0 with no warnings. The `pyqt6` extra exists back to napari 0.6.2, the minimum allowed version.

Found via the scverse integration tests (scverse/spatialdata-integration-testing#26).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75b8c346bee6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
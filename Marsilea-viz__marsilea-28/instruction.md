# Issue

**Title:** Correct the typo related to the order of `FixedChunk` parameters

## Description

Correct the typo related to the order of `FixedChunk` parameters.

Code Snippet:
```
import marsilea as ma
import numpy as np
from marsilea.plotter import FixedChunk

matrix = np.random.randn(20, 20)

h = ma.Heatmap(matrix)

chunk = ['C1', 'C2', 'C3', 'C4']

labels = np.random.choice(chunk, size=20)


h = ma.Heatmap(matrix)
chunk = ['C1', 'C2-1', 'C2-2', 'C4']
labels = np.random.choice(chunk, size=20)
h.hsplit(labels=labels, order=chunk)
h.add_right(FixedChunk(chunk, bordercolor="gray"), pad=.1)
h.add_right(FixedChunk(['C1', 'C2', 'C3'],
                       ratio=[1, 2, 1], fill_colors="red"), pad=.1)
h.render()
```

Before:
```
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[1], [line 21](vscode-notebook-cell:?execution_count=1&line=21)
     [18](vscode-notebook-cell:?execution_count=1&line=18) h.add_right(FixedChunk(chunk, bordercolor="gray"), pad=.1)
     [19](vscode-notebook-cell:?execution_count=1&line=19) h.add_right(FixedChunk(['C1', 'C2', 'C3'],
     [20](vscode-notebook-cell:?execution_count=1&line=20)                        ratio=[1, 2, 1], fill_colors="red"), pad=.1)
---> [21](vscode-notebook-cell:?execution_count=1&line=21) h.render()

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:807](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:807), in ClusterBoard.render(self, figure, scale)
    [805](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:805) self.figure = figure
    [806](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:806) self._freeze_legend(figure)
--> [807](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:807) self._freeze_flex_plots(figure)
    [809](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:809) # Make sure all axes is split
    [810](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:810) self._setup_axes()

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:394](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:394), in WhiteBoard._freeze_flex_plots(self, figure)
    [392](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:392) for plan in self._col_plan + self._row_plan:
    [393](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:393)     if plan.size is None:
--> [394](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:394)         render_size = plan.get_canvas_size(figure)
    [395](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:395)         if render_size is not None:
    [396](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/base.py:396)             self.layout.set_render_size(plan.name, render_size)

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:382](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:382), in _LabelBase.get_canvas_size(self, figure)
    [381](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:381) def get_canvas_size(self, figure):
--> [382](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:382)     self.texts_size = self.silent_render(figure, expand=self.get_expand())
    [383](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:383)     return self.texts_size + self.padding / 72

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:371](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:371), in _LabelBase.silent_render(self, figure, expand)
    [369](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:369) for s, c in zip(self.texts, locs):
    [370](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:370)     x, y = (0, c) if self.is_flank else (c, 0)
--> [371](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:371)     t = ax.text(x, y, s=s, transform=ax.transAxes, **params.to_dict())
    [372](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:372)     bbox = t.get_window_extent(renderer).expanded(*expand)
    [373](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/marsilea/plotter/text.py:373)     if self.is_flank:

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:689](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:689), in Axes.text(self, x, y, s, fontdict, **kwargs)
    [628](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:628) """
    [629](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:629) Add text to the Axes.
    [630](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:630) 
   (...)
    [679](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:679)     >>> text(x, y, s, bbox=dict(facecolor='red', alpha=0.5))
    [680](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:680) """
    [681](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:681) effective_kwargs = {
    [682](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:682)     'verticalalignment': 'baseline',
    [683](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:683)     'horizontalalignment': 'left',
   (...)
    [687](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:687)     **kwargs,
    [688](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:688) }
--> [689](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:689) t = mtext.Text(x, y, text=s, **effective_kwargs)
    [690](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:690) t.set_clip_path(self.patch)
    [691](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/axes/_axes.py:691) self._add_text(t)

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:454](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:454), in make_keyword_only.<locals>.wrapper(*args, **kwargs)
    [448](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:448) if len(args) > name_idx:
    [449](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:449)     warn_deprecated(
    [450](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:450)         since, message="Passing the %(name)s %(obj_type)s "
    [451](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:451)         "positionally is deprecated since Matplotlib %(since)s; the "
    [452](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:452)         "parameter will become keyword-only %(removal)s.",
    [453](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:453)         name=name, obj_type=f"parameter of {func.__name__}()")
--> [454](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/deprecation.py:454) return func(*args, **kwargs)

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:183](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:183), in Text.__init__(self, x, y, text, color, verticalalignment, horizontalalignment, multialignment, fontproperties, rotation, linespacing, rotation_mode, usetex, wrap, transform_rotates_text, parse_math, **kwargs)
    [167](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:167) self._text = ''
    [168](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:168) self._reset_visual_defaults(
    [169](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:169)     text=text,
    [170](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:170)     color=color,
   (...)
    [181](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:181)     rotation_mode=rotation_mode,
    [182](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:182) )
--> [183](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:183) self.update(kwargs)

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:231](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:231), in Text.update(self, kwargs)
    [229](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:229) # Update bbox last, as it depends on font properties.
    [230](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:230) bbox = kwargs.pop("bbox", sentinel)
--> [231](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:231) super().update(kwargs)
    [232](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:232) if bbox is not sentinel:
    [233](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:233)     self.set_bbox(bbox)

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1213](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1213), in Artist.update(self, props)
   [1205](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1205) def update(self, props):
   [1206](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1206)     """
   [1207](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1207)     Update this artist's properties from the dict *props*.
   [1208](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1208) 
   (...)
   [1211](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1211)     props : dict
   [1212](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1212)     """
-> [1213](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1213)     return self._update_props(
   [1214](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1214)         props, "{cls.__name__!r} object has no property {prop_name!r}")

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1199](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1199), in Artist._update_props(self, props, errfmt)
   [1196](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1196)             if not callable(func):
   [1197](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1197)                 raise AttributeError(
   [1198](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1198)                     errfmt.format(cls=type(self), prop_name=k))
-> [1199](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1199)             ret.append(func(v))
   [1200](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1200) if ret:
   [1201](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/artist.py:1201)     self.pchanged()

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1010](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1010), in Text.set_horizontalalignment(self, align)
   [1000](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1000) def set_horizontalalignment(self, align):
   [1001](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1001)     """
   [1002](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1002)     Set the horizontal alignment relative to the anchor point.
   [1003](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1003) 
   (...)
   [1008](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1008)     align : {'left', 'center', 'right'}
   [1009](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1009)     """
-> [1010](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1010)     _api.check_in_list(['center', 'right', 'left'], align=align)
   [1011](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1011)     self._horizontalalignment = align
   [1012](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/text.py:1012)     self.stale = True

File [~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/__init__.py:131](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/__init__.py:131), in check_in_list(_values, _print_supported_values, **kwargs)
    [129](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/__init__.py:129) if _print_supported_values:
    [130](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/__init__.py:130)     msg += f"; supported values are {', '.join(map(repr, values))}"
--> [131](https://vscode-remote+ssh-002dremote-002blocalhost.vscode-resource.vscode-cdn.net/public/home/liuzj/notebooks/mouseBrain/20230830_restart/~/softwares/anaconda3/envs/mouseNN/lib/python3.8/site-packages/matplotlib/_api/__init__.py:131) raise ValueError(msg)

ValueError: 'red' is not a valid value for align; supported values are 'center', 'right', 'left'
```

After:
![图片](https://github.com/Marsilea-viz/marsilea/assets/55271666/d36392ea-588e-406f-87b9-161f4bb0d31e)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `473f485f685e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
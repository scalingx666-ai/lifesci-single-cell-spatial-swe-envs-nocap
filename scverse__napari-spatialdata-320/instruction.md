# Issue

**Title:** Fix instance id shift bug; fix obsm viz; fix background color labels

## Description

Fixed:
- bugs with `layer.properties`:
    - on mouse hover the layer properties were not shown (this was visible in previous `napari-spatialdata` versions)
    - the correct instance property is now shown; properties were shown for the wrong instance, as reported in #242. 
    - This is available for all the types of annotations `obs`, `var`, `obsm` and dataframe columns.
    - Available for points and labels. Not for shapes, see issue in `napari`: 
- plotting a continuous variable on a labels caused:
	- the background color to be black instead of transparent; now it's transparent
	- the first instance (no matter which index, for instance `2`) to be black, instead of being of a different color
- plotting variables on `obsm` was not working
- the coloring of categorical variables via pre-saved colors was not working because there was a `"_color"` instead of `"_colors"`
- there were some imprecisions in the tests for the scatterplot widget:
	- the table was not parsed using `TableModel`
	- an unused (and wrong) `region_key` parameter was passed; I removed it
- some modifications in the docs; in particular I warn the user that when zooming in on points in macOS one needs to be careful when looking at the values of points on mouse hover. In fact points that seem to be far away could still be overlapping. Example here: 

Missing (I will track these are new issues)
- tests for plotting data from `obsm`
- tests for hovering with the mouse and checking that the status bar of the viewer shows the correct value

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8df1eb632b4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
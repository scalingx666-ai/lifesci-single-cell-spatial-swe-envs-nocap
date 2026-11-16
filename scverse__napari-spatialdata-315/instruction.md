# Issue

**Title:** Add functions to interactive

## Description

As discussed with @LucaMarconato @melonora and @josenimo, I added two small functions to annotate the shapes/visualize the sample id. The two functions are:

1. `get_layer` grabs the layer name and returns the layer if it matches the user input. 
2. `add_text_to_polygons` adds annotations/sample names visually to the chosen polygons/shapes layer

When the user visualizes their data, annotations or simple sample id's could help in identifying samples and aid in analysis. 
Example usage would be: 

```
sample_id_list = gdf.index.tolist()
polygon_layer_name = 'Control'
interactive.add_text_to_polygons(polygon_layer_name, text_annotations)
```
1. Grab the sample id from the GeoDataFrame (index is used by default when linking a table with a shapes element)
2. Define the shapes layer (name of the spatial element shapes)
3. annotate (for now the default is: font size 10, red, center)

Ideally it will look like this:
![image](https://github.com/user-attachments/assets/defdb3e1-73c3-4165-9dbe-fe44b9db785b)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d49c2388850`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
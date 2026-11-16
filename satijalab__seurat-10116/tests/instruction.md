# Issue

**Title:** Package-wide fix of `aes_string`

## Description

Hi Seurat Team, 

@anashen also tagging you directly here as you followed up on previous PR regarding `aes_string`.

This is pretty wide one following up on #9409 to address use of `aes_string` package wide.  This is not 100% complete as I will explain and have couple things to draw attention to.  I have checked the visualization functions manually as best I can but definitely should have another set of eyes test them to see if anything breaks before merge.

Most of the fixes for this were very straightforward and had no issues but wanted to let team know about couple specific instances of note.

### **Not currently working:  Interactive version of `SpatialPlot`**  

The regular version of `SpatialPlot` seems to work just fine for both features and clusters/groups.  The interactive plot renders just fine actually but when you bring mouse to hover over it repeatedly prints this warning:
```
Warning: Error in nearPoints: nearPoints: `xvar` ('.data[["y"]]')  not in names of input
```

If you then try and click as you would to select region the window goes dark and you have to manually stop the interactive plot.

Not sure if it's relevant but `CellSelector` works just fine on regular `DimPlot`.

I'm not as familiar with interactive plotting so not really sure what's going on here but can dig into it.  But figured I would create push now in case it's just easy fix for someone who knows the interactive plotting a little better than me.


### **Things of Note:**  
Most of the fixes for this were very straightforward and had no issues but wanted to let team know about couple specific instances of note.

Seurat now imports `data_sym` and `data_syms` from rlang.  There are few use cases for this were relevant.
- First is when some variables provided in `aes` could be NULL.
This is the case in `SingleDimPlot` for instance here:  
https://github.com/samuel-marsh/seurat/blob/1df6ebaf02ef2ba924ba4116c183a095458b79da/R/visualization.R#L8653C2-L8671C6  

The fix for that is implemented as discussed in  and .


- Another time this is done is as replacement for what I assume was way to safely name variables that had incompatible characters by enclosing them in backticks.
This is the case for instance in `SingleExiPlot` (from current main branch):
```
x <- paste0("`", feature, "`") 
```

This has been updated to:
```
y <- data_sym(feature)
```
and then uses `!!` in the `ggplot` call for those variables.

If safe naming was not the original intent and/or this fix doesn't serve desired purpose let me know.

- Anotherl note is as part of `SingleSpatialPlot` with the following line of code:
```
col.by <- col.by %iff% paste0("`", col.by, "`")
```

Again I used the fix involving `data_sym` and `!!` in the ggplot2 call.  However, I also had to create additional variable `col.by.plot` as `col.by` gets called later in the function as part of `gsub` call and if I directly modified `col.by` with `data_sym` it caused failure there.
```
col.by.plot <- col.by %iff% data_sym(col.by)
```


- Final note is in `SingleImagePlot` where the following was originally inside `aes_string`:
```
fill = col.by %NA% NULL
```

However fixing with `.data[[col.by]] %NA% NULL` didn't correctly evaluate and led to legend being named "ident %NA%" so I created additional variable and combine with solution from first note and use `data_syms` to safely pass including if NULL.



That's about it but please let me know if there are any issues or additional changes to make here.  And again I'll also look into interactive spatial plot issue but figured I'd post this now in case it's easy fix for someone who knows that better.

Thanks again for all you do!
Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db9a3fbff25a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
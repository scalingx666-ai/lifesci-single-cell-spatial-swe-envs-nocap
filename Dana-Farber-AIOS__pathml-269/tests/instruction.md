# Issue

**Title:** Bioformats multichannel bug

## Description

When we added support for multi-level images with BioFormatsBackend in #251, we broke our support for images which store channels as series (i.e. those from the MISI lab).

As a workaround, we add a flag `series_as_channels` to `BioFormatsBackend.extract_region()` which can be used to work with these types of images. 

In my testing, this works (the test checks whether all the channels of the returned array are the same, so a result of False is good):

````python
# test reading region from a TIFF from Schurch et al
im_path = Path("data/reg031_X01_Y01.tif")
bf = BioFormatsBackend(str(im_path))
im = bf.extract_region(location=(1000, 1000), size=100)
print(all([np.array_equal(im[:, :, :, 0, :], im[:, :, :, i, :]) for i in range(1, im.shape[3])]))

>>> False

# test reading a misi image with channels stored in series, using the new flag
im_path_misi = Path("data/MISI3590i_CTMA_117_AD_Scan2_Core[11,16,E]_[12878,56504]_component_data.tif")
bf_misi = BioFormatsBackend(str(im_path_misi))
im_misi = bf_misi.extract_region(location=(1000, 1000), size=100, series_as_channels = True)
print(all([ np.array_equal(im_misi[:, :, :, 0, :], im_misi[:, :, :, i, :]) for i in range(1, im_misi.shape[3])]))

>>> False

# test reading a multi-level .scn image to make sure we keep support for multi-level functionality
im_path_multilevel_scn = Path("../data/Leica-3.scn")
bf_multilevel = BioFormatsBackend(str(im_path_multilevel_scn))
im_multilevel_level0 = bf_multilevel.extract_region(location=(0, 0), size=bf_multilevel.shape_list[0][0:2], level=0)
im_multilevel_level4 = bf_multilevel.extract_region(location=(0, 0), size=bf_multilevel.shape_list[4][0:2], level=4)
print(all([ np.array_equal(im_multilevel_level0[:, :, :, 0, :], im_multilevel_level0[:, :, :, i, :]) for i in range(1, im_multilevel_level0.shape[3])]))
print(all([ np.array_equal(im_multilevel_level4[:, :, :, 0, :], im_multilevel_level4[:, :, :, i, :]) for i in range(1, im_multilevel_level4.shape[3])]))

>>> False
>>> False
````

This should resolve #261 

## Testing

One problem that this highlighted is that our testing suite needs to be improved.

Ideally, I think we should test all these scenarios (at minimum) for the BioFormatsBackend:
- standard tiff (like the one from Schurch et al)
- multi-level image
- MISI tiff to make sure we support them

I tested these above manually, but we should really include them in the test suite. However, we want to minimize the size of the files in our testing suite, so we can't include an 8GB image from schurch et al. or a 2GB multi-level image from the openslide example data. 

Ideally we should include a wide range of image types of minimal size, e.g. of dims (4, 4, 4, 4, 4). I tried cropping these images but haven't had success so far. FIJI crop function seemed to only crop the single plane I was one, and I couldn't get bioformats.write_image() to work. @ryanccarelli  thoughts?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a24e71fe5a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
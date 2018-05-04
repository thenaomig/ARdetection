# ARdetection
The atmospheric river detection algorithm used in Goldenson et al. (2018, submitted).

The algorithm takes as input a 2D field (total column integrated precipitable water, or vertically integrated vapor flux), for some subset of latitudes and longitudes in the extratropics. It has primarily been tested for a box that extends from near Hawaii on the lower left to encompass Alaska and the West Coast of North America. A threshold value of 2cm precipitable water is used in this example, and in Goldenson et al. (2018), to mask the data, which is empirically appropriate for the region in question.

Feature detection built into the multi-dimensional image processing library <A href="https://docs.scipy.org/doc/scipy/reference/ndimage.html">SciPy.ndimage</A> is used to identify contiguous regions that exceed the masked threshold. Subsequent tests ensure the feature is >2000km in length and <1000km in width, and that the it intersects the coast in a geographic region of interest. 

Using the Python library <A href="http://xarray.pydata.org/en/stable/">xarray</A> we can scale this process, grouping data by time so that the detection can be done in parallel for all of the time-intervals desired. It works best to point to one large file with all of the data across time, or files of equal size, so that the data will be chunked in optimal fashion. 

The 2D fields can be provided at daily or sub-daily frequency. In this example, 6-hourly data is averaged to daily frequency before applying the algorithm ('hasAR'). 

The algorithm has been tested on climate model output and the ERA-Interim and MERRA2 reanalyses.

The example <A href="https://jupyter.org">jupyter notebook</A> presented here, using Python 2.7, shows the application of the algorithm to the ERA-Interim reanalysis. A land-sea mask and manually-input gridcell spacing is all that is needed to customize this to any dataset.

If you use or adapt this algorithm, please acknowledge that you have done so and also contact me, as I will be interested to hear about it.

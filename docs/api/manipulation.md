---
layout: default
title: cpc.geogrids.manipulation module
type: apidoc
---
        
# cpc.geogrids.manipulation Module
> Contains methods for interpolating data between GeoGrids.



## Functions

### <span class="function">fill_outside_mask_borders(data, passes=1)</span> 

> Fill the grid points outside of the mask borders of a dataset (eg. over the ocean for
> land-only datasets) with the value from the nearest non-missing neighbor
> 
> ### Parameters
> 
> - data - *numpy array* - data to fill missing
> - passes - *int* - number of passes (for each pass, 1 extra layer of grid points will be
> filled)
> 
> ### Returns
> 
> - *numpy array* - a filled array
> 
> ### Examples
> 
> Create a 5x5 array of data, mask out the outer values, and fill
> 
>     >>> # Import packages
>     >>> from cpc.geogrids.manipulation import fill_outside_mask_borders
>     >>> import numpy as np
>     >>> # Generate random data with missing values along the border
>     >>> A = np.random.randint(1, 9, (5, 5)).astype('float16')
>     >>> A[0] = A[-1] = A[:,0] = A[:,-1] = np.nan
>     >>> A  # doctest: +SKIP
>     array([[ nan,  nan,  nan,  nan,  nan],
>            [ nan,   4.,   4.,   3.,  nan],
>            [ nan,   6.,   7.,   3.,  nan],
>            [ nan,   3.,   8.,   8.,  nan],
>            [ nan,  nan,  nan,  nan,  nan]], dtype=float16)
>     >>> # Fill the missing outside values with the nearest neighbor values
>     >>> A = fill_outside_mask_borders(A)
>     >>> A  # doctest: +SKIP
>     array([[ 4.,  4.,  4.,  3.,  3.],
>            [ 4.,  4.,  4.,  3.,  3.],
>            [ 6.,  6.,  7.,  3.,  3.],
>            [ 3.,  3.,  8.,  8.,  8.],
>            [ 3.,  3.,  8.,  8.,  8.]], dtype=float16)



### <span class="function">grid_to_stn(gridded_data, grid, stn_lats, stn_lons)</span> 

> Interpolates values from a grid to stations in a station list.
> 
>     Parameters
>     ----------
> 
>     - gridded_data (array_like)
>         - Array of gridded data
>     - grid (Grid)
>         - `data_utils.gridded.grid.Grid` that the gridded data is on
>     - stn_lats (list)
>         - List of station lats
>     - stn_lons (list)
>         - List of station lons
> 
>     Returns
>     -------
> 
>     - list
>         - List of values representing the value of the gridded data interpolated to the station
>           locations
> 
>     Examples
>     --------



### <span class="function">interpolate(orig_data, orig_grid, new_grid)</span> 

> Interpolates data from one Geogrid to another.
> 
> ### Parameters
> 
> - orig_data - *array_like* - array of original data
> - orig_grid - *Geogrid* - original Geogrid
> - new_grid - *Geogrid* - new Geogrid
> 
> ### Returns
> 
> - new_data - *array_like* - a data array on the desired Geogrid.
> 
> ### Examples
> 
> Interpolate gridded temperature obs from 2 degrees (CONUS) to 1 degree global
> 
>     #!/usr/bin/env python
>     >>> # Import packages
>     >>> import numpy as np
>     >>> from cpc.geogrids.definition import Geogrid
>     >>> from cpc.geogrids.manipulation import interpolate
>     >>> # Create original and new GeoGrids
>     >>> orig_grid = Geogrid('1deg-global')
>     >>> new_grid = Geogrid('2deg-global')
>     >>> # Generate random data on the original Geogrid
>     >>> A = np.random.rand(orig_grid.num_y, orig_grid.num_x)
>     >>> # Interpolate data to the new Geogrid
>     >>> B = interpolate(A, orig_grid, new_grid)
>     >>> # Print shapes of data before and after
>     >>> print(A.shape)
>     (181, 360)
>     >>> print(B.shape)
>     (91, 180)



### <span class="function">smooth(data, grid, factor=0.5)</span> 

> Smooth an array of spatial data using a gaussian filter
> 
> ### Parameters
> 
> - data - *array_like* - array of spatial data
> - grid - *Geogrid* - Geogrid corresponding to data
> - factor - *float, optional* - sigma value for the gaussian filter
> 
> ### Returns
> 
> - *array_like* - array of smoothed spatial data
> 
> ### Examples



# Raster operations in R

<table class="package_ver_table">
<tbody>
  <tr>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> R </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> raster </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> tmap </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> sf </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> gdistance </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> ggplot2 </td>
   <td style="text-align:left;color: black !important;background-color: #ffc178 !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> rasterVis </td>
  </tr>
  <tr>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 4.1.1 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 3.4.13 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 3.3.2 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 1.0.2 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 1.3.6 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 3.3.5 </td>
   <td style="text-align:left;color: white !important;background-color: #AAAAAA !important;text-align: center;font-size: 12px !important; 
              margin:5px; 
              border-radius: 8px;
              border: 2px solid white;
              padding-top: 1px;
              padding-bottom: 1px;
              padding-left: 4px;
              padding-right: 4px;"> 0.50.3 </td>
  </tr>
</tbody>
</table>

## Sample files for this exercise {-}

We'll first load spatial objects used in this exercise from a remote website: an elevation `raster` object, a bathymetry `raster` object and a continents `sf` vector object 


```r
load(url("http://github.com/mgimond/Spatial/raw/master/Data/raster.RData"))
```

Both rasters cover the entire globe. Elevation below mean sea level are encoded as `0` in the elevation raster. Likewise, bathymetry values above mean sea level are encoded as `0`.

Note that most of the map algebra operations and functions covered in this tutorial are implemented using the `raster` package. See chapter 10 for a theoretical discussion of map algebra operations.

## Local operations and functions {-}

### Unary operations and functions (applied to single rasters) {-}

Most algebraic operations can be applied to rasters as they would with any vector element. For example, to convert all bathymetric values in `bath` (currently recorded as positive values)  to *negative* values simply multiply the raster by `-1`.


```r
library(raster)

bath2 <- bath * (-1)
```

Another unary operation that can be applied to a raster is reclassification. In the following example, we will assign all `bath2` values that are less than zero a `1` and all zero values will remain unchanged. A simple way to do this is to apply a conditional statement.


```r
bath3 <- bath2 < 0
```

Let's look at the output. Note that all `0` pixels are coded as `FALSE` and all `1` pixels are coded as `TRUE`.


```r
library(tmap)
tm_shape(bath3) + tm_raster(palette = "Greys") + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-5-1.png" width="672" />

If a more elaborate form of reclassification is desired, you can use the `reclassify` function. In the following example, the raster object `bath` is reclassified to 4 unique values: 100, 500, 1000 and 11000 as follows:

Original depth values | Reclassified values
--------------------- | -------------------
0 - 100               | 100
101 - 500             | 500
501 - 1000            | 1000
1001 - 11000          | 11000

The first step is to create a plain matrix where the first and second columns list the starting and ending values of the range of input values that are to be reclassified, and where the third column lists the new raster cell values.


```r
m <- c(0, 100, 100,  100, 500, 500,  500, 
       1000,  1000, 1000, 11000, 11000)
m <- matrix(m, ncol=3, byrow = T)
m
```

```
     [,1]  [,2]  [,3]
[1,]    0   100   100
[2,]  100   500   500
[3,]  500  1000  1000
[4,] 1000 11000 11000
```


```r
bath3 <- reclassify(bath, m, right = T)
```

The `right=T` parameter indicates that the intervals should be closed to the right (i.e. the second column of the reclassification matrix is inclusive).


```r
tm_shape(bath3) + tm_raster(style="cat") + tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-8-1.png" width="672" />

You can also assign `NA` (missing) values to pixels. For example, to assign `NA` values to cells that are equal to 100, type


```r
bath3[bath3 == 100] <- NA
```

The following chunk of code highlights all `NA` pixels in grey and labels them as missing.


```r
tm_shape(bath3) + tm_raster(showNA=TRUE, colorNA="grey") + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-10-1.png" width="672" />

### Binary operations and functions (where two rasters are used) {-}

In the following example, `elev` (elevation raster) is added to `bath` (bathymetry raster) to create a single elevation raster for the globe. Note that the bathymetric raster will need to be multiplied by `-1` to differentiate above mean sea level elevation from below mean sea level depth.


```r
elevation <- elev - bath
```


```r
tm_shape(elevation) + tm_raster(palette="-RdBu",n=6) + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-12-1.png" width="672" />

## Focal operations and functions {-}

Operations or functions applied focally to rasters involve user defined neighboring cells. For example, a cell output value can be the average of all 121 cells--an 11x11 kernel--centered on the cell whose value is being estimated (this is an example of a _smoothing function_).


```r
f1 <- focal(elevation, w=matrix(1,nrow=11,ncol=11)  , fun=mean)
```


```r
tm_shape(f1) + tm_raster(palette="-RdBu",n=6) + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-14-1.png" width="672" />

By default edge cells are assigned a value of `NA`. This is because cells outside of the input raster extent have no value but may fall inside the kernel window when edge cells are computed. You can remedy this by passing the parameters `na.rm=TRUE` and `pad=TRUE` to the function.


```r
f1 <- focal(elevation, w=matrix(1,nrow=11,ncol=11)  , 
            fun=mean, pad=TRUE,  na.rm = TRUE)
```


```r
tm_shape(f1) + tm_raster(palette="-RdBu",n=6) + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-16-1.png" width="672" />

But, you must be careful when making use of the `na.rm=TRUE`/`pad=TRUE` combination. In the above example, we are passing the values from the kernel window as *a vector element* to the `mean` function.  So the number of valid (non NA) values being passed to the `mean` function does not matter since the function will sort out the weights based on the number of input values.

If, however, the smoothing function makes use of explicitly defined weights, then setting `pad=TRUE` will be problematic since the edge pixels will succumb to unbalanced weights. In the following example, we'll compare the output of three 3x3 smoothing operations as follows: 


```r
# Using the mean function
f_mean     <- focal(elevation, w=matrix(1,nrow=3,ncol=3), fun=mean, na.rm=TRUE, pad=TRUE)

# Using explicitly defined weights
f_wt_nopad <- focal(elevation, w=matrix(1/9,nrow=3,ncol=3), na.rm=TRUE, pad=FALSE)
f_wt_pad   <- focal(elevation, w=matrix(1/9,nrow=3,ncol=3), na.rm=TRUE, pad=TRUE)
```

The following images are zoomed in on the upper left-hand set of pixels of each raster output. The `elevation` raster is the input raster.

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-18-1.png" width="768" />

The left-most image shows the original upper left-hand corner elevation pixel values. The second image shows the output using the mean function with the `pad=TRUE` option. The third image shows the output using the weighted kernel window with the `pad=FALSE` option (note the upper row of `NA` pixels highlighted in *bisque* color). The last image shows the output from the same weighted kernel window using the `pad=TRUE` option. This last outcome is not desirable. For example, the middle top pixel is computed from `1/9(-4113 -4113 -4112 -4107 -4104 -4103)`, which results in dividing the sum of *six* values by *nine*--hence the unbalanced weight effect. Note that we do not have that problem using the mean function. 

You might have noticed the lack of edge effect issues along the western edge of the raster outputs. This is because the `focal` function will wrap the eastern edge of the raster to the western edge of that same raster if the input raster layer spans the entire globe (i.e from -180 &deg; to +180 &deg;).


The _neighbors_ matrix (or _kernel_) that defines the moving window can be customized. For example if we wanted to compute the average of all 8 neighboring cells _excluding_ the central cell we could define the matrix as follows:


```r
m  <- matrix(c(1,1,1,1,0,1,1,1,1)/8,nrow = 3) 
f2 <- focal(elevation, w=m, fun=sum)
```

More complicated kernels can be defined. In the following example, a [Sobel][2] filter (used for edge detection in image processing) is defined then applied to the raster layer `elevation`.


```r
Sobel <- matrix(c(-1,0,1,-2,0,2,-1,0,1) / 4, nrow=3) 
f3    <- focal(elevation, w=Sobel, fun=sum) 

tm_shape(f3) + tm_raster(palette="Greys") + 
  tm_legend(legend.show = FALSE) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-20-1.png" width="672" />

## Zonal operations and functions {-}

A common zonal operation is the aggregation of cells. In the following example, raster layer `elevation` is aggregated to a 5x5 raster layer.


```r
z1 <- aggregate(elevation, fact=2, fun=mean, expand=TRUE)

tm_shape(z1) + tm_raster(palette="-RdBu",n=6) + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-21-1.png" width="672" />

The image may not look much different from the original, but a look at the image properties will show a difference in pixel sizes.


```r
res(elevation)
```

```
[1] 0.3333333 0.3333333
```

```r
res(z1)
```

```
[1] 0.6666667 0.6666667
```

`z1`'s pixel dimensions are half of `elevation`'s dimensions. You can reverse the process by using the `disaggregate` function which will split a cell into the desired number of subcells while assigning each one the same parent cell value.

Zonal operations can often involve two layers, one with the values to be aggregated, the other with the defined zones. In the next example, `elevation`'s cell values are averaged by zones defined by the `cont` polygon layer.

The following chunk computes the mean elevation value for each unique polygon in `cont`,


```r
cont.elev.sp <- extract(elevation, cont, fun=mean, sp=TRUE) 
```

The `sp=TRUE` parameter instructs the function to output a `SpatialPolygonsDataFrame` object (same as the input zonal object) instead of a standalone table (matrix). The output spatial object inherits the original attributes and adds a column called `layer` with the computed mean elevation values.

We can convert the `SpatialPolygonsDataFrame` object to an `sf` vector object for flexibility.


```r
library(sf)
cont.elev <- st_as_sf(cont.elev.sp)
```

The average elevation can be extracted from the `sf` object as follows:


```r
st_drop_geometry(cont.elev)
```

```
      CONTINENT     layer
1        Africa  630.6706
2    Antarctica 2342.8605
3     Australia  276.5497
4        Europe  262.7817
5 North America  826.0598
6 South America  595.4753
7          Asia  790.6417
```
 
If you are working off of the original `SpatialPolygonsDataFrame` vector object, use the `cont.elev.sp@data` syntax to extract the dataframe.

We can now map the average elevation by continent.


```r
tm_shape(cont.elev) + tm_polygons(col="layer") + 
  tm_legend(outside = TRUE, text.size = .8)
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-26-1.png" width="672" />

Many custom functions can be applied to `extract`. For example, to extract the maximum elevation value by continent, type:


```r
cont.elev.sp <- extract(elevation, cont, fun=max, sp=TRUE) 
```

As another example, we may wish to extract the number of pixels in each polygon using a customized function. 


```r
cont.elev.sp <- extract(elevation, cont, fun=function(x,...){length(x)}, sp=TRUE) 
```

The `extract` function will also work with lines and point spatial objects. If you wish to compute the zonal statistics of a raster using another raster as zones instead of a vector layer, use the `zonal()` function instead.

## Global operations and functions {-}

Global operations and functions may make use of all input cells of a grid in the computation of an output cell value.

An example of a global function is the Euclidean distance function, `distance`,  which computes the shortest distance between a pixel and a source (or destination) location. To demonstrate the `distance` function, we'll first create a new raster layer with two non-NA pixels.


```r
r1   <- raster(ncol=100, nrow=100, xmn=0, xmx=100, ymn=0, ymx=100)
r1[] <- NA              # Assign NoData values to all pixels
r1[c(850, 5650)] <- 1   # Change the pixels #850 and #5650  to 1
crs(r1) <- "+proj=ortho"  # Assign an arbitrary coordinate system (needed for mapping with tmap)
```


```r
tm_shape(r1) + tm_raster(palette="red") + 
  tm_legend(outside = TRUE, text.size = .8) 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-30-1.png" width="672" />

Next, we'll compute a Euclidean distance raster from these two cells. The output extent will default to the input raster extent.


```r
r1.d <- distance(r1) 
```


```r
tm_shape(r1.d) + tm_raster(palette = "Greens", style="order", title="Distance") + 
  tm_legend(outside = TRUE, text.size = .8) +
  tm_shape(r1) + tm_raster(palette="red", title="Points") 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-32-1.png" width="672" />

You can also compute a distance raster using `SpatialPoints` objects or a simple x,y data table. In the following example, distances to points (25,30) and (87,80) are computed for each output cell. However, since we are working off of point objects (and not an existing raster as was the case in the previous example), we will need to create a blank raster layer which will define the extent of the Euclidean distance raster output. 


```r
# Create a blank raster
r2 <- raster(ncol=100, nrow=100, xmn=0, xmx=100, ymn=0, ymx=100)
crs(r2) <- "+proj=ortho"  # Assign an arbitrary coordinate system 

# Create a point layer
xy <- matrix(c(25,30,87,80),nrow=2, byrow=T) 
p1 <- SpatialPoints(xy)
crs(p1) <- "+proj=ortho"  # Assign an arbitrary coordinate system 
```

Now let's compute the Euclidean distance to these points using the `distanceFromPoints` function.


```r
r2.d <- distanceFromPoints(r2, p1)
```

Let's plot the resulting output.


```r
tm_shape(r2.d) + tm_raster(palette = "Greens", style="order") + 
  tm_legend(outside = TRUE, text.size = .8) +
  tm_shape(p1) + tm_bubbles(col="red") 
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-35-1.png" width="672" />

## Computing cumulative distances {-}

This exercise demonstrates how to use functions from the `gdistance` package to generate a cumulative distance raster. One objective will be to demonstrate the influence "adjacency cells" wields in the final results.

Load the `gdistance` package.


```r
library(gdistance)
```

First, we'll create a 100x100 raster and assign a value of `1` to each cell. The pixel value defines the cost (other than distance) in traversing that pixel. In this example, we'll assume that the cost is uniform across the entire extent. 


```r
r   <- raster(nrows=100,ncols=100,xmn=0,ymn=0,xmx=100,ymx=100)
r[] <- rep(1, ncell(r))
```







If you were to include traveling costs other than distance (such as elevation) you would assign those values to each cell instead of the constant value of `1`. 

A **translation matrix** allows one to define a 'traversing' cost  going from one cell to an adjacent cell. Since we are assuming there are no 'costs' (other than distance) in traversing from one cell to any adjacent cell we'll assign a value of 1, `function(x){1}`, to the translation between a cell and its adjacent cells (i.e. translation cost is uniform in all directions).
 
There are four different ways in which 'adjacency' can be defined using the `transition` function. These are showcased in the next four blocks of code.

In this example, adjacency is defined as a **four node** (vertical and horizontal) connection (i.e. a "rook" move). 

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-40-1.png" width="288" style="display: block; margin: auto auto auto 0;" />


```r
h4   <- transition(r, transitionFunction = function(x){1}, directions = 4)
```

In this example, adjacency is defined as an **eight node** connection (i.e. a single cell "queen" move).

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-42-1.png" width="288" style="display: block; margin: auto auto auto 0;" />


```r
h8   <- transition(r, transitionFunction = function(x){1}, directions = 8)
```

In this example, adjacency is defined as a  **sixteen node** connection (i.e. a single cell "queen" move combined with a "knight" move).

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-44-1.png" width="288" style="display: block; margin: auto auto auto 0;" />


```r
h16  <- transition(r, transitionFunction=function(x){1},16,symm=FALSE)
```

In this example, adjacency is defined as a **four node diagonal** connection (i.e. a single cell "bishop" move).

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-46-1.png" width="288" style="display: block; margin: auto auto auto 0;" />


```r
hb   <- transition(r, transitionFunction=function(x){1},"bishop",symm=FALSE)
```

The `transition` function treats all adjacent cells as being at an equal distance from the source cell across the entire raster.  `geoCorrection` corrects for 'true' local distance. In essence, it's adding an additional cost to traversing from one cell to an adjacent cell (the original cost being defined using the `transition` function). The importance of applying this correction will be shown later. 

Note: `geoCorrection` also corrects for distance distortions associated with data in a geographic coordinate system. To take advantage of this correction, make sure to define the raster layer's coordinate system using the `projection` function.





```r
h4    <- geoCorrection(h4,  scl=FALSE)
h8    <- geoCorrection(h8,  scl=FALSE)
h16   <- geoCorrection(h16, scl=FALSE)
hb    <- geoCorrection(hb,  scl=FALSE)
```

In the "queen's" case, the diagonal neighbors are $\sqrt{2 x (CellWidth)^{2}}$ times the cell width distance from the source cell.

Next we will map the cumulative distance (`accCost`) from a central point (A) to all cells in the raster using the four different adjacency definitions.


```r
A       <- c(50,50) # Location of source cell
h4.acc  <- accCost(h4,A)
h8.acc  <- accCost(h8,A)
h16.acc <- accCost(h16,A)
hb.acc  <- accCost(hb,A) 
```

If the `geoCorrection` function had not been applied in the previous steps, the cumulative distance between point location A and its neighboring adjacent cells would have been different. Note the difference in cumulative distance for the 16-direction case as shown in the next two figures.

Uncorrected (i.e. `geoCorrection` _not_ applied to h16):

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-51-1.png" width="288" style="display: block; margin: auto auto auto 0;" />

Corrected (i.e. `geoCorrection`  applied to h16):

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-52-1.png" width="288" style="display: block; margin: auto auto auto 0;" />

The "bishop" case offers a unique problem: only cells in the diagonal direction are identified as being adjacent. This leaves many undefined cells (labeled as `Inf`). We will change the `Inf` cells to `NA` cells. 


```r
hb.acc[hb.acc == Inf] <- NA
```

Now let's compare a 7x7 subset (centered on point A) between the four different cumulative distance rasters. 

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-54-1.png" width="576" style="display: block; margin: auto auto auto 0;" />

To highlight the differences between all four rasters, we will assign a red color to all cells that are within 20 cell units of point A.

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-55-1.png" width="576" style="display: block; margin: auto auto auto 0;" />




It's obvious that the accuracy of the cumulative distance raster can be greatly influenced by how we define adjacent nodes. The number of red cells (i.e. area identified as being within a 20 units cumulative distance) ranges from 925 to 2749 cells.

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-57-1.png" width="672" />

### Working example {-}
In the following example, we will generate a raster layer with barriers (defined as `NA` cell values). The goal will be to identify all cells that fall within a 290 km traveling distance from the upper left-hand corner of the raster layer (the green point in the maps). Results between an 8-node and 16-node adjacency definition will be compared.


```r
# create an empty raster
r   <- raster(nrows=300,ncols=150,xmn=0,ymn=0,xmx=150000, ymx=300000)

# Define a UTM projection (this sets map units to meters)
projection(r) = "+proj=utm +zone=19 +datum=NAD83" 

# Each cell is assigned a value of 1
r[] <- rep(1, ncell(r)) 

# Generate 'baffles' by assigning NA to cells. Cells are identified by
# their index and not their coordinates.
# Baffles need to be 2 cells thick to prevent the 16-node
# case from "jumping" a one pixel thick NA cell.
a <- c(seq(3001,3100,1),seq(3151,3250,1))
a <- c(a, a+6000, a+12000, a+18000, a+24000, a+30000, a+36000)
a <- c(a , a+3050)
r[a] <- NA

# Let's check that the baffles are properly placed
tm_shape(r) + tm_raster(colorNA="red") + 
  tm_legend(legend.show=FALSE)

# Next, generate a transition matrix for the 8-node case and the 16-node case
h8   <- transition(r, transitionFunction = function(x){1}, directions = 8)
h16  <- transition(r, transitionFunction = function(x){1}, directions = 16)

# Now assign distance cost to the matrices. 
h8   <- geoCorrection(h8)
h16  <- geoCorrection(h16)

# Define a point source and assign a projection
A <- SpatialPoints(cbind(50,290000))
crs(A) <- "+proj=utm +zone=19 +datum=NAD83 +units=m +no_defs"  

# Compute the cumulative cost raster
h8.acc   <- accCost(h8, A)
h16.acc  <- accCost(h16,A)

# Replace Inf with NA
h8.acc[h8.acc   == Inf] <- NA
h16.acc[h16.acc == Inf] <- NA
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-58-1.png" width="672" style="display: block; margin: auto auto auto 0;" />

Let's plot the results. Yellow cells will identify cumulative distances within 290 km.


```r
tm_shape(h8.acc) + tm_raster(n=2, style="fixed", breaks=c(0,290000,Inf)) +
  tm_facets() + tm_shape(A) + tm_bubbles(col="green", size = .5) + 
  tm_legend(outside = TRUE, text.size = .8)

tm_shape(h16.acc) + tm_raster(n=2, style="fixed", breaks=c(0,290000,Inf)) + 
  tm_facets() + tm_shape(A) + tm_bubbles(col="green", size = .5) + 
  tm_legend(outside = TRUE, text.size = .8)
```

<img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-59-1.png" width="672" style="display: block; margin: auto auto auto 0;" /><img src="A06-Raster-Operations_files/figure-html/unnamed-chunk-59-2.png" width="672" style="display: block; margin: auto auto auto 0;" />

We can compute the difference between the 8-node and 16-node cumulative distance rasters:


```r
table(h8.acc[]  <= 290000) 
```

```

FALSE  TRUE 
31458 10742 
```

```r
table(h16.acc[] <= 290000)
```

```

FALSE  TRUE 
30842 11358 
```




The number of cells identified as being within a 290 km cumulative distance of point A for the 8-node case is 10742 whereas it's 11358 for the 16-node case, a difference of 5.4%.

[1]: http://en.wikipedia.org/wiki/Dana_Tomlin
[2]: http://en.wikipedia.org/wiki/Sobel_operator


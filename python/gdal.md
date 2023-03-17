#### installing gdal using conda (recommended)
`conda install -c conda-forge gdal`
#### installing gdal using .whl file
`python -m pip install path-to-wheel-file.whl`

### read/write and simple operations raster files
```py
ds = gdal.Open("<filename>")
```

#### get projection and transformation
```py
ds.GetProjection()
ds.GetGeoTransform()
```

#### get band values as arrays
```py
band = ds.GetRasterBand(1)
array = band.ReadAsArray()
```

#### use array values to plot
```py
plt.figure()
plt.imshow(array)
```

#### manipulate (mask)
```py
binmask = np.where((array >= np.mean(array)),1,0)
plt.imshow(binmask)
```

#### export (example)
```py
driver = gdal.GverByName("GTiff")
driver.Register()
outds = driver.Create("binmask.tif", xsize = binmask.shape[1],
                      ysize = binmask.shape[0], bands = 1, 
                      eType = gdal.GDT_Int16)
outds.SetGeoTransform(gt)
outds.SetProjection(proj)
outband = outds.GetRasterBand(1)
outband.WriteArray(binmask)
outband.SetNoDataValue(np.nan)
outband.FlushCache()
```

#### close datasets and bands
```py
outband = None
outds = None
````

#### convert raster data between different formats
- `gdal.translate(<src_dataset>, <dst_dataset>)` if no arguments are given, format readable by pandas is created




#### rasterize (convert vector to rasters)
- `gdal_rasterize -ts 100 100 -a_nodata -9999 -burn 1 face.shp face.tif`

#### you can create a new one or overlap

#### polygonize
- `gdal_polygonize.py <raster_filename> <vector_filename>` 


## processing vector data with gdal (ogr is now part of gdal)
- `ogrinfo -so <name_of_shp>`
- `ogr2ogr -of KML <output_name> <input_name>` convert shp to kml
- `ogr2ogr -where "FID>3" <output_name> <input_name>` convert shp to shp with filters
- `ogr2ogr -t_srs epsg:32422 shp2UTM.shp output.shp`
- `ogr2ogr merged.shp shp1.shp`
- `ogr2ogr -append -update merged.shp shp2UTM.shp -nln merged`
- `ogr2ogr -sql "SELECT OGR_GEOM_AREA AS area FROM merged" area.shp merge.shp`

### convert between csv and GeoTIFF with GDAL in Python
```py
from osgeo import gdal
import pandas as pd
import numpy as np
import os
import matplotlib.pyplot as plt

ds = gdal.Open("dem.tif")

# TIFF to CSV 
# first option
xyz = gdal.Translate("dem.xyz", ds) #copies the file
xyz = None

df = pd.read_csv("dem.xyz", sep = " ", header = None)
df.columns = ["x","y", "value"]
df.to_csv("dem.csv", index = False)

# second option
ar = ds.GetRasterBand(1).ReadAsArray()
flat = ar.flatten()
gt = ds.GetGeoTransform()
res = gt[1]
xmin = gt[0]
ymax = gt[3]
xsize = ds.RasterXSize
ysize = ds.RasterYSize
xstart = xmin + res/2
ystart = ymax - res/2
ds = None

x = np.arange(xstart, xstart + xsize * res,  res)
y = np.arange(ystart, ystart - ysize * res, -res)
x = np.tile(x, ysize)
y = np.repeat(y, xsize)

dfn = pd.DataFrame({"x":x, "y":y, "value":flat})

# CSV to TIFF
# first option
dfn.to_csv("dfn.xyz", index = False, header = None, sep = " ")
demn = gdal.Translate("demn.tif", "dfn.xyz", outputSRS = "EPSG:32719")
demn = None

def toTIFF(dfn, name):
    dfn.to_csv(name+".xyz", index = False, header = None, sep = " ")
    demn = gdal.Translate(name+".tif", name+".xyz", outputSRS = "EPSG:32719", 
                          xRes = res, yRes = -res)
    demn = None
    
shuffle = dfn.sample(frac = 1)
shuffle = shuffle.sort_values(by = ["y", "x"], ascending = [False, True])
toTIFF(shuffle, "shuffle")

sample = dfn.sample(frac = 0.1)
sample = sample.sort_values(by = ["y", "x"], ascending = [False, True])
toTIFF(sample, "sample")

uneven = sample.copy()
uneven.x = uneven.x + np.random.randint(6, size = len(uneven))
uneven.y = uneven.y + np.random.randint(6, size = len(uneven))
# toTIFF(uneven, "uneven") # not working 

# second option
uneven.to_csv("uneven.csv", index = False)
if os.path.exists("uneven.vrt"):
    os.remove("uneven.vrt")

f = open("uneven.vrt", "w")
f.write()
f.close()

r = gdal.Rasterize("uneven.tif", "uneven.vrt", outputSRS = "EPSG:32719", 
                          xRes = res, yRes = -res, attribute = "value", noData = np.nan)
r = None

g = gdal.Grid("unevenInt.tif", "uneven.vrt", outputSRS = "EPSG:32719")
g = None
```

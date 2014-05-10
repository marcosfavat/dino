[GDAL](http://gdal.org/) is a popular and powerful geospatial data processing library. Importing a DEM with the help of GDAL gives exactly the same result than the standard mode but provides 2 main advantages:

* Process any GIS raster data format that Blender can't natively read
* Process large raster data source

Importing data through GDAL allows to create from any GIS raster datasource an image that can be easily imported in Blender. **GDAL option always produces a new file and pack it in Blender.** Afterward, this new image is used to config the displacer with exactly the same process used in standard mode.

Using GDAL needs beforehand to correctly [install it](https://github.com/domlysz/BlenderGIS/wiki/Install-GDAL).

**Notes about how the data is pre-processing through GDAL**

* The DEM will be automatically clip according to the working extent, it's why it's possible to work with large datasource
* You can process any raster bit depth but the output will be always force to 16 bits. So if your data is coded into 32 bits integer or floating values you will loss accuracy.
* A worldfile isn't necessary needed (some GIS formats simply don't need it because georeferencing informations is stored in a different way)
* No data pixels are set to zero

**Tool options are very close to the standard DEM import**

![](https://github.com/domlysz/BlenderGIS/raw/master/images/georaster_Mode_As_DEM_GDAL.jpeg)

* *GDAL mode* : the script can uses GDAL in 2 different ways
    * by send commands to GDAL binaries
    * by using GDAL python API

    For the moment, these two modes give exactly the same result. But Python API is more versatile and evolutionary for new future features.

* *Objects* : with this list you can select the mesh that will be used to config the displacer. Usually this is the reference map image previously imported on a plane.

* *Subdivision* : Subdivision is needed because the displacer needs some vertices to work with. The script can subdivise the plane by adding a simple subsurf modifier or by cutting the plane according to the number of DEM pixel which overlay the mesh.

* *Scale* : check this if you want to [scale](https://github.com/domlysz/BlenderGIS/wiki/Scale-DEM-dataset) the raster

* *Angular coords* : check this if the raster is in [decimal degrees](https://github.com/domlysz/BlenderGIS/wiki/Working-in-decimal-degrees)




If you need to deal with GIS specific raster format and process it with GDAL, think to disable the filter.

![](https://github.com/domlysz/BlenderGIS/raw/master/images/georaster_DEM_GDAL_disable_filter.jpg)

Note that the process creates temporary files (in Blender temp. folder) which will be removed later.
QGIS is open source software that can help you to visualize, understand and process your geodata.

Here some tips:

**How generate a worldfile when it does not exist**

Menu *Raster > Projections > Extract projection*

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/qgis_extract_wf.jpg)

**How to clip a raster which is too large extent**

The best way to do it is the *save raster as* dialog.

* First move and zoom the QGIS map view canvas to encompass the extent of interest.
* Right click on layer and choose save raster as. In the dialog, click on map view extent button.
* In create options add *tfw=yes*, in this way QGIS creates the world file needed for blender import.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/qgis_saveAs_clip.jpg)

Another way to clip a raster is the clipper tool under *Raster menu > Extraction > Clipper*. Think to add *–co tfw=yes* option in the gdal command to get the worldfile.

**How to know the raster bit depth**

Just check it in the raster metadata panel in layer properties.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/qgis_metadata_bitDepth.jpg)

**How to get raster min/max statistics**

Look at raster medata to check if some statistics are already computed.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/qgis_metadata_Stats.jpg)

If statistics doesn’t exist you can also compute the values in the style panel. The advantage of this way is that you can compute stats for full extent or current map view extent.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/qgis_properties_stats.jpg)

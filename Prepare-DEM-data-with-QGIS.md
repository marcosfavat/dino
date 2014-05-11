If you cannot or don’t want using GDAL options, you need a good knowledge of your data and maybe some pre-processing to ensure the import in Blender.

Here some tips:

**How generate a worldfile when it does not exist**

Menu *Raster / Projections / Extract projection*

**How to clip a raster which is too large extent**

The best way to do it is the save raster as dialog.

* First move and zoom the QGIS map view canvas to encompass the extent of interest.
* Right click on layer and choose save raster as. In the dialog, click on map view extent button.
* In create options add worldfile=yes, in this way QGIS creates the world file needed for blender import.

Another way to clip a raster is the clipper tool under raster menu / Extraction / Clipper. Think to add –co tfw=yes option in the gdal command to get the worldfile.

**How to know the raster bit depth**

Just check it in the raster metadata.

**How to decrease raster bit depth from 32 bits to 16 bits**

The addon cannot handle correctly 32 bits raster dataset, so you need to decrease the bit depth to 16 bits, but note that you will lose data accuracy. To do it use gdal_ranslate tool

You need to edit the command to add some options:
-co worldfile=yes -> creates a worldfile, which will be useful for the import into blender
-ot UInt16 -> indicates the data type (UInt16 = unsigned 16 bits, Int16 = signed 16 bits, Byte = 8 bits)

You can also add -scale option if you want to rescale the pixels values according to the bit depth range capacity. For example if elevation values are from 0 to 350 and your data in 16 bits (max value = 65535) then just type **-scale 0 350 0 65535** (values from 0 to 350 will be stretch from 0 to 65535)
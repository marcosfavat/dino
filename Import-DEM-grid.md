The *As DEM* mode can be used to import a raster that define a Digital Elevation Model where each pixel values of the image represents a true elevation. This type of raster, also called grid, is usually composed of one band that can be coded into different bit depth depending on the data accuracy:

Bit depth             |   Range of values that each pixel can contain
----------------------|-----------------------------------
1 bit                 |   0 to 1
2 bit                 |   0 to 4
4 bit                 |   0 to 16
Unsigned 8 bit        |   0 to 255
Signed 8 bit          |   -128 to 127
Unsigned 16 bit       |   0 to 16
Signed 16 bit         |   -32768 to 32767
Unsigned 32 bit       |   0 to 4294967295
Signed 32 bit         |   -2147483648 to 2147483647
Floating-point 32 bit |   -3.402823466e+38 to 3.402823466e+38

The best way to use this kind of data for warp a mesh in Blender is by setting a Displace modifier.This modifier displaces vertices in a mesh based on the intensity of a texture.

For the moment, the script can only process 8 or 16 bit raster because it seems the displacer cannot correctly deal with 32 bits integer or floating DEM.

Before import a DEM you need a mesh to apply the displacer on. Standard workflow is to import beforehand a texture map like topographic map or aerial photo on a plane. This plane will define the working area and will be used as reference for the DEM import.

Then you can launch the DEM import tool. The dimensions of the reference plane and the extent of the DEM dataset don't need to be exactly the same. You can use, without worrying, a DEM smaller or larger than the plane because the script will compute UV mapping according to the georeferencing data so in all cases overlay will be correct.

There are several option available :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_Mode_As_DEM.jpeg)

* *Objects* : with this list you can select the mesh that will be used to config the displacer. Usually this is the reference map image previously imported on a plane.

* *Subdivision* : Subdivision is needed because the displacer needs some vertices to work with. The script can subdivise the plane by adding a simple subsurf modifier or by cutting the plane according to the number of DEM pixel which overlay the mesh.

* *Image depth* : you need to specify original DEM bit depth. This information is needed to retrieve pixel elevation values because Blender texture value is normalized from 0.0 to 1.0. You can easily find this  information with QGIS for example.

* *Is scaled* : check this if the raster is [scaled](https://github.com/domlysz/BlenderGIS/wiki/Scale-DEM-dataset)

    Using scaled DEM requires the user to specify what are original maximum and minimum elevation of the raster dataset because this information is no longer available once the values have been re-distributed.

    ![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_Mode_As_DEM_Is_Scaled.jpeg)

* *Angular coords* : check this if the raster is in [decimal degrees](https://github.com/domlysz/BlenderGIS/wiki/Working-in-decimal-degrees)

After the import you must see the mesh correctly warped

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_DEM_result.jpeg)

In the modifier stack you can check the displace setting

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_Displacer_Settings.jpeg)

**To increase the warp effect the best way is to edit the object dimension Z property but you will loose true elevation**

The DEM is used as texture for the displacer and to place this texture the mesh as now a new UV map calculates according to the DEM overlay position.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_Mesh_UVmap.jpeg)

**Strength calculation:**   
The strength value defines the vertex displacement  
`Displacement = (Texture value - Midlevel) × Strength`  
Midlevel represents texture value which will be treated as no displacement by the modifier, for convenience it is always set to zero, so  
`Strength = Displacement / Texture value`  
Where displacement is the target elevation change (altitude max - altitude min) and texture value is Blender color value which is normalize between 0.0 and 1.0. A Blender texture value of 1.0 equal to the maximum value that can be assigned in the raster dataset, so this value depends on raster bit depth  
`texture value = delta Z / (2^depth-1)`  
Finally  
`Strength = delta Z / (delta Z / (2^depth-1))`  
**`Strength = 2^depth-1`**

The script also sets some important parameters of the displacer texture:

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georaster_Displacer_texture_Settings.jpeg)

The _As DEM_ mode can be used to import a raster that define a Digital Elevation Model where each pixel values of the image represents a true elevation. This type of raster, also called grid, is usually composed of one band that can be coded into different bit depth depending on the data accuracy:

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

The best way to use this kind of data in Blender is by setting a Displace modifier.This modifier displaces vertices in a mesh based on the intensity of a texture.

For the moment, the script can only process 8 or 16 bit raster because it seems the displacer cannot correctly deal with 32 bits integer or floating DEM.

Before import a DEM you need a mesh to apply the displacer on. Standard workflow is to import beforehand a texture map like topographic map or aerial photo on a plane. This plane will define the working area and will be used as reference for the DEM import.

There are several option available :

*_Objects_ : with this list you can select the mesh that will be used to config the displacer. Usually this is the reference map image previously imported on a plane.

*_Subdivision_ : Subdivision is needed because the displacer needs some vertices to work with. The script can subdivise the plane by adding a simple subsurf modifier or by cutting the plane according to the number of DEM pixel which overlay the mesh.

*_Warp method_ : there are two ways to get the displacement : by setting the strength value of the displacer or by setting the object dimension Z property. It's more meaningful for the user to play with obj dimension Z because strength values depends on raster bit depth and doesn't simply represent elevation change. 

Bellow some technical notes about strength calculation:
The strength value defines the vertex displacement
->_Displacement = (Texture value - Midlevel) × Strength_<-
Midlevel represents texture value which will be treated as no displacement by the modifier, for convenience it is always set to zero, so 
->So _Strength = Displacement / Texture value_<-
Where displacement is the target elevation change (altitude max - altitude min) and texture value is Blender color value which is normalize between 0.0 and 1.0. A Blender texture value of 1.0 equal to the maximum value that can be assigned in the dataset, so this value depends on raster bit depth
->_texture value = delta Z / (2^depth -1)_<-
Finally : _Strength = delta Z / (delta Z / (2^depth -1)) = **2^depth-1**_

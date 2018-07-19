# **I'm trying to import a DEM file but Blender become completely freezing, what happened ?**

DEM dataset can be extremely huge covering thousand of kilometers with a very high resolution, while on the other hand Blender is not designed to handle this kind of large dataset. Futhermore, geographic data can be in various formats, projections or extents, and most of the time to get a smooth import in blender you'll need to perform some preprocessing tasks.

Consider exploring you geographic data and understand its properties as an absolutely essential task before trying any import. Especially for raster Digital Elevation Models there are some important properties to know about:

* **number of pixels :** it will give you the number of vertices in Blender. Use common sense here : is it a reasonnable number or billions ?
* **geographic extent covered in comparison to your desired working extent :** most of the time you'll have only need a small part of your DEM file
* **projection system and unit :** projection have lot of consequensies and really need your consideration. You need to know what is the projection of your file and if this projection is suitable for your work or not
* **size of one pixel in projection unit :** is it too much or too low in comparason to your expected level of detail ?
* **data type (int16, uint16, float32 ...) :** importing unsigned 16 bits as DEM texture involves an extra conversion step which can be very slow


You can use QGIS, to explore you data beforehand. QGIS is a powerful open source desktop GIS software, this is an essential tool for working with BlenderGIS, it will not only help you to undersand you data but it's also a swiss knife able to perform any king of processing tasks you'll need like:

* reprojection in a coordinnate system in meters
* cliping to the desired working extent
* resampling to a lower pixel resolution
* nodata values filling

Some of these tasks can be handled directly in BlenderGIS, but the most straightforward strategy is generally to prepare your data beforehand with the help of QGIS.

# **Why after the import of my data the resulting mesh is extremely small on x and y axis but seems correct on Z axis ?**

Geodata often distributed in a geographic coordinate system rather in a metric one. It means that x and y represents the angular coordinates longitude and latitude of the point location on the sphere earth. Angular coordinates are in degrees not in meters, in other words x and y axis does not share the same unit than z axis. The earth perimeter is about 40 000 km so one degree at equator represents 40000km / 360° = 111km and one meter equal about 0.00001°, that's why x and y values are so small comparing to z values.

# **Ok then, what can I do ?**

You must transform your data in a projection system in meters, and so, you must determine what is the best projection for your location. Each country has his own set of legal projection system. The reprojection task can be performed with QGIS in preference but BlenderGIS, in a lesser extent, can also handle heterogenous projection system. To deal with different projection system in BlenderGIS you must correctly set up the projection of the scene (which represents the destination system) and the projection of your input dataset.

# **Why my measurements on basemaps reference seems wrong ?**

Again this is related to the projection system. Most of basemaps layers are served into Web Mercator projection. The Mercator projection can represents the whole sphere earth but it makes this possible at the cost of significant distortions : the size of objects increases as the latitude increases from the Equator to the poles. This linear scale factor is applyied equally in all directions making the projection conformal (angles are preserved).

https://en.wikipedia.org/wiki/Mercator_projection#Distortion

Multiplying the measured distance by `cos(lat)` gives an approximation of the true distance. For exemple at latitude 45°, the measurment of 4000 meters represents in fact 3140 meters. That why for precision modeling the web mercator projection is not suitable.
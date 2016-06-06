This tool can import in Blender most of shapefile feature type : point, pointZ, polyline, polylineZ, polygon, polygonZ. But actually it cannot import multipoint, multipointZ, pointM, polylineM, polygonM and multipatch.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_options.jpg)


**Troubles**

* This tool depends on pyshp library that is in beta version, so sometimes it cannot process the shapefile. Typically, if you got "Unable to read shapefile", "Unable to extract geometry" or "Unable to read DBF table" error, these are pyShp issues. In this case:

    * Try to check if there is any update of [pyshp lib](http://code.google.com/p/pyshp/downloads/list).

    * If there is no update available or if update doesn't correct the problem, try to open and re-export the shapefile with any GIS software. You can also try to clean/repair geometry, delete unnecessary fields...

* For polygons import, if you see faces which seem to be strangely filled try to remove duplicate vertex on the mesh (modify tolerance distance if necessary)

* The script can handle multipart geometry but actually if the part defines a polygon hole, a face will still be created.

* Because the scene can be very large, don’t forget to configure camera clipping distance according to the scene. If you still see black faces error on render image after setting clip end distance try to set the clip start distance closer to the scene, it will help Blender to improve vertex position according to the Z depth of the camera.
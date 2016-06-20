Remember BlenderGIS is building with the mind of a 2 step workflow :

1. Explore and manage your data in your favourite GIS software
2. Try to import them in Blender

Following this paradigm BlenderGIS always make the assumption you have a good knowledge on what you are trying to import, if it's not the case please go to step 1.

You must also read carefully [how BlenderGIS handle georeferencing informations](https://github.com/domlysz/BlenderGIS/wiki/Gereferencing-management).

*****

This tool can import in Blender most of shapefile feature type : point, pointZ, polyline, polylineZ, polygon, polygonZ. But actually it cannot import multipoint, multipointZ, pointM, polylineM, polygonM and multipatch.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_options.jpg)

### Elevation and extrusion

wiki in progress ...


### Coordinate Reference System (CRS)

When importing a shapefile it's necessary to specify the projection of the file.

Typical import workflow assumes 2 mains conditions:
- all your data must be already in the same projection
- this projection must be suitable for your area of interest.

Once again use a GIS software to explore and manage your data (reprojection, clip ...) before trying to import them in Blender. Each contry have a set of commonly used projections, if you really don't know if the projection of your data is suitable for your location you can consider transforming them into the right [UTM](https://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system) zone. However, this topic is out of scope of BlenderGIS wiki.


Most of shapefile define the CRS in a .prj file witch contains the definition of the projection in [Well-know text (wkt) format](https://en.wikipedia.org/wiki/Well-known_text). However, BlenderGIS store map projection as [SRID](https://en.wikipedia.org/wiki/Spatial_reference_system#Identifier) unique identifier and unfortunaly discover the right SRID from WKT definition is not an easy task. Futhermore, the prj file is optional and may be missing. That's why for now the user must explicit the input/file SRS.


Fortunaly, BlenderGIS handle a list of predefinate CRS witch help to quickly specify the projection of your input data.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_srs.jpg)

If the CRS of your input file is not in the list, you can quickly add a new one with `+` operator.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_srs_add.jpg)

You can find more information on how to manage this list of predefinate CRS in [*geoscene* addon documentation](https://github.com/domlysz/BlenderGIS/wiki/Gereferencing-management#geoscene-addon).

**Warning :**

**You must avoid as much as possible importing a shapefile stored as longitude/latitude in degrees otherwise you will lose data accuracy.** One degree on the earth is equals to approx 111km so one meter is approx 0.00001 degrees but Blender works with coordinates as single precision (float32) and a single float value has actually about 7 significant digits of precision. You cannot expect an accuracy bellow 1 meter when working in decimal degrees because closest points will be rounded and merged into one. Futhermore, angulars units will be virtually unusable in Blender. In this case, you need to choose an appropriate map projection (in linear units) for your location and transform your data into this reference system.


### Reprojection capabilities

Shapefile importer support minimal reprojection capabilities which can be usefull in some case. **Please use this functionnaly with caution and full background knowledge, BlenderGIS can't do magic alignment for you...**

Reprojection will be involved each time a shapefile must be transformed to match the scene CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_reproj_ex.jpg)

The scene CRS is the destination CRS so it leads all reprojection tasks. If the scene is not yet georeferenced, then it will be not possible to perform a reprojection task.

Georeferencing informations of the scene will be automatically initialized according to the first shapefile import. But, it's possible to define the scene CRS before importing any shapefile and thus ensure reprojection of each subsequent imports. To do this use the [geoscene manager](https://github.com/domlysz/BlenderGIS/wiki/Gereferencing-management#Geoscene-addon) panel available in 3dview tool sheft.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)


### Troubles

* This tool depends on pyshp library that is in beta version, so sometimes it cannot process the shapefile. Typically, if you got "Unable to read shapefile", "Unable to extract geometry" or "Unable to read DBF table" error, these are pyShp issues. In this case:

    * Try to check if there is any update of [pyshp lib](http://code.google.com/p/pyshp/downloads/list).

    * If there is no update available or if update doesn't correct the problem, try to open and re-export the shapefile with any GIS software. You can also try to clean/repair geometry, delete unnecessary fields...

* For polygons import, if you see faces which seem to be strangely filled try to remove duplicate vertex on the mesh (modify tolerance distance if necessary)

* The script can handle multipart geometry but actually if the part defines a polygon hole, a face will still be created.

* Because the scene can be very large, don’t forget to configure camera clipping distance according to the scene. If you still see black faces error on render image after setting clip end distance try to set the clip start distance closer to the scene, it will help Blender to improve vertex position according to the Z depth of the camera.

Delaunay triangulation is suitable for create a 3D surface from points cloud or contour lines generally obtained from a topographical survey.

This type of vector representation of land surface is usually called [Triangulated irregular network](http://en.wikipedia.org/wiki/Triangulated_irregular_network) (TIN).

***Triangulation from heterogeneous points cloud***

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/delaunay_from_heterogeneous_points_cloud.jpg)

***Triangulation from contour lines***

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/delaunay_from_contours.jpg)

***Triangulation from DEM regular points cloud***

Using Delaunay triangulation can also be a strategy to create a TIN from a DEM raster dataset. In this case, the workflow is the following:
* convert the DEM raster into point features (shapefile) with any GIS software  
* import the shapefile in Blender
* triangulate the points cloud

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/shp_import_DEM_points_cloud.jpg)

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/delaunay_DEM_points_cloud.jpg)

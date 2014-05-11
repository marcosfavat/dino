Delaunay triangulation is suitable for create a 3D surface from points cloud or contour lines generally obtained from a topographical survey

This type of vector representation of land surface is usually called [Triangulated irregular network](http://en.wikipedia.org/wiki/Triangulated_irregular_network) (TIN).

Using Delaunay triangulation can also be a strategy to create a TIN from a DEM raster dataset. In this case, the workflow is the following:
* convert the DEM raster into point features (shapefile) with any GIS software  
* import the shapefile in Blender
* triangulate the points cloud

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_DEM_points_cloud.jpg)

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/delaunay_DEM_points_cloud.jpg)
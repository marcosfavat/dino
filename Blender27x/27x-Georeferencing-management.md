## Custom properties

For storing georeferencing informations, BlenderGIS creates some custom properties in the scene:

- **Coordinate Reference System (CRS)** *also called Spatial Reference System (SRS)*

A map is commonly built through a cartographic projection which transforms angular coordinates on earth's surface to planar coordinates and allows the representation of a territory that minimize distortions or preserves certain properties.

It's essential to know which CRS is in use to store and represent the geodata you want to import, because mixing data in different CRS's is not possible without reprojection capabilities.

The Spatial Reference Identifier (SRID) is an unique value used to unambiguously identify a coordinate reference system. SRID is in the form AUTHORITY:CODE but most of the time authority is just EPSG because the large majority of commonly used CRS's are defined in the widely used EPSG database.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_srid.jpg)

- **Scene origin geolocation**

Blender (and most 3d software) cannot handle objects well that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64).

That's why it's necessary to create the mesh near to the scene origin. To avoid loss georeferencing accuracy, custom properties are used to keep track of scene origin coordinates.

The most universal way to store the geolocation of a point is as angular coordinates : longitude and latitude.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_lonlat.jpg)

However, referring to longitude and latitude is not enough; we need to know the map's projection and how to convert from angular coordinates to the projected system (and vice versa), which involve reprojection capabilities through complex formulas and external software. That's why storing the scene origin coordinates directly in its map projection system can be a better choice.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_xy.jpg)

BlenderGIS manages in priority the CRS coordinates of the scene's origin and updates the corresponding longitude/latitude if it can to do the math. Keeping angular coordinates up to date is necessary to ensure compatibility with other addons which require storing scene origin as longitude latitude.

- **Map scale denominator**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_scale.jpg)

This is an essential property if you want to build a map that covers a large territory while maintaining in Blender a reasonable scene area.


## Geoscene addon

*Geoscene* is a special addon extensively used by other BlenderGIS addons and which offers useful functionality to deal with georeferencing information.


- **Predefined CRS's**

The *Geoscene* addon offers the ability to define, save and manage a set of predefined Coordinate Reference Systems (CRS).

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpg)

Adding a new predefined CRS is really easy, thanks to the http://epsg.io/ service it's possible to perform a simple keyword search.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpg)

*Note for advanced user: instead of a SRID, it's possible to use a proj4 string to define a CRS.*

The predefined CRS list is used each time we need to specify a projection system. For example when importing a shapefile or a georaster it is necessary to set the CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_predef_crs_example.jpg)

Predefining the most common projection systems used by your data will be subsequently very helpfull to quickly set an input CRS.

- **Georef manager**

This manager is accessible from the 3dview tool shelf.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel2.jpg)

The panel reflects the current state of the geoscene:
- What is the scene CRS ?
- Is the scene origin geolocation set ? As longitude/latitude or in CRS space or both ?
- Is it usuable or broken ?

When a scene is not yet georeferenced, then most of BlenderGIS addons will automatically initialize the CRS and origin geolocation as needed, for example at first import (shapefile or georaster) or when starting the basemaps addon.

A scene is considered correctly georeferenced when at least a valid CRS is defined and the coordinates of scene's origin in this CRS space is set. On the other hand a geoscene will be broken if the origin is set but not the CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpg)

Furthermore, if the origin is only set as longitude/latitude the geoscene still remains broken. However, there is a dedicated operator to update projected coordinates from angulars coordinates and vice versa.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin2.jpg)


Through the manager, it's also possible to switch the scene CRS. When enabling this mode, the panel displays the list of predefined CRS's and an operator button to validate the change.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)

When the CRS is updated, the addon also tries to update the origin coordinates to the new CRS space.
**Be carefull, updating the CRS will not reproject the elements previously imported. Be aware of this risk when changing the CRS.**

- **Reprojection capabilities**


The *geoscene* addon offers reprojection functionnalities used by other BlenderGIS addons.

Transforming coordinates from one CRS to another is a complex task, especially given the wide variety of projection system available. Fortunately, [Proj4](https://en.wikipedia.org/wiki/PROJ.4) is a powerful open-source library that can be used to reproject coordinates between CRS's.

However, BlenderGIS is built to be usuable as a dependency-free addon. It always tries to offer minimum functionality without any painful installation of extra Python modules.

BlenderGIS can perform CRS transformations through different approaches depending on available modules and requested CRS's:
- It provides some built-in Python functions to perfom usefull common transformation, but they support only few CRS transformation.
- http://epsg.io/ offers a great web service to transform coordinates between EPSG code. It will be used by BlenderGIS to provide minimum reprojection support between a wide variety of systems. However, requesting the service is slow and therefore is not suitable to transform lot of coordinates.
- BlenderGIS can use any of the two main Python interfaces to proj4 : [GDAL OGR](https://pypi.python.org/pypi/GDAL/) or [pyproj](https://pypi.python.org/pypi/pyproj?). If one of these modules is available then it will be used to perform all reprojection tasks.

Reprojection will be involved each time a coordinate or a dataset must be transformed to match the scene CRS. So, because the scene CRS leads all reprojection tasks, it must be carefully choosen to minimize transformation requests as much as possible. **It's a good idea to harmonize your data to the same CRS through a dedicated software like QGIS before trying to import them in Blender.**


- **For developers**

The *GeoScene* class is a simple Python interface to manage custom scene properties. Using this class instead of directly setting the property is easier and offers more control (input validation, update triggers ...).

The georef manager panel is built as a reusuable layout that can be easily append to another addon layout.

The *geoscene* addon also register a set of operators to perform common usefull tasks to manage georef informations.

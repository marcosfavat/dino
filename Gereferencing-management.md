## Custom properties

For storing georeferencing informations, BlenderGIS creates some custom properties in the scene:

- **Spatial Reference System (SRS)** *also called Coordinate Reference System (CRS)*

A map is commonly building through a cartographic projection witch transform angular coordinates on earth surface to planar coordinates and allows the representation of a territory that minimize distoritions or preserve some properties.

It's essential to know what is the SRS in use to store and represent the geodata you want to import, because mixing data in differente SRS is not possible without reprojection capabilities.

The Spatial Reference Identifier (SRID) is an unique value used to unambiguously identify a coordinate reference system. SRID is in the form AUTHORITY:CODE but most of the time authory just refer to EPSG because the large majority of commonly used SRS are defined in the widely used EPSG database


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_srid.jpg)

- **Scene origin geolocation**

Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64).

That's why it's necessary to create the mesh near to the scene origin. For avoid georeferencing lost, custom properties are used to keep track of scene origin coordinates.

The most universal way to store the geolocation of a point is as angular coordinates : longitude and latitude.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_lonlat.jpg)

However, refering to longitude and latitude is not enough, we need to know what's the map projection and to be able to convert from angulars coordinates to this projected system (and vice versa) which involve reprojection capabilities through complex formulas and external software. That's why storing the scene origin coordinates directly in it's map projection system can be a better choice.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_xy.jpg)

BlenderGIS manage in priority the SRS coordinates of scene origin and update the corresponding longitude/latitude if it can to do the math. Maintening angular coordinates up to date is useful to ensure compatibility with orthers addons witch prefers storing scene origin as longitude latitude.

- **Map scale denominator**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_scale.jpg)

This is an essential property if you want building a map that cover a large territory while maintaining in Blender a reasonable scene area.


## Geoscene addon

*Geoscene* is a special addon extensively used by others BlenderGIS addons and which offers useful functionnalities to deal with georeferencing information.


- **Predefinate CRS**

*Geoscene* addon offers the possibility to define, save and manage a set of predefined Coordinate Reference System (CRS).

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpg)

Adding a new predefined CRS is really easy, thanks to http://epsg.io/ service it's possible to perfom a simple keyword search.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpg)

*Note for advanced user: instead of a SRID, it's possible to use a proj4 string to define a to CRS.*

The predifinate CRS list is used each time we need to specify a projection system. For example when importing a shapefile or a georaster it's necessary to define what is the input CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_predef_crs_example.jpg)

Predefining the most common projection systems used by your data will be subsequently very helpfull to quickly set an input CRS.

- **Georef manager**

This manager is accessible from 3dview tool sheft.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel2.jpg)

The panel reflects the current state of the geoscene:
- What is the scene CRS ?
- Is the scene origin geolocation set ? As longitude/latitude or in CRS space or both ?
- Is it usuable or broken ?

A scene is considered correctly georeferenced when at least a valid CRS is defined and the coordinates of scene's origin in this CRS space is set. On the other hand a geoscene will be broken if the origin is set but not the CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpg)

Furthermore, if the origin is only set as longitude/latitude the geoscene still remains broken. However, there is a dedicated operator to update projected coordinates from angulars coordinates and vice versa.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin2.jpg)


Through the manager, it's also possible to switch the scene CRS. When enabling this mode, the panel diplay the list of predefinates CRS and an operator button to validate the change.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)

When the CRS is updated, the addon try to also update the origin coordinates to the new CRS space.
**Be carefull, updating the CRS will not reproject the data previously imported, change it with full background knowledge of risk.**

- **Reprojection capabilities**


The *geoscene* addon offers reprojection functionnalities used by others BlenderGIS addons.

Transforming coordinates from a CRS to another is a complex task especially given the wide variety of projection system available. Fortunately, [Proj4](https://en.wikipedia.org/wiki/PROJ.4) is a strong open-source library that can be used to reproject coordinates between SRS.

However, BlenderGIS is building to be usuable as a dependance free addon. It try to always offers minimum functionnalities without any painfull installation of extra Python modules.

BlenderGIS can performs CRS transformation through differents way depending on available modules and requested CRS :
- It provides some built-in Python functions to perfom usefull common transformation, but they support only few CRS transformation.
- http://epsg.io/ offers a great web service to transform coordinates between EPSG code. It will be used by BlenderGIS to provide minimum reprojection support between a wide variety of systems. However, requesting the service is slow and therefore is not suitable to transform lot of coordinates.
- BlenderGIS can use any of the two main Python interface to proj4 : [GDAL OSR](https://pypi.python.org/pypi/GDAL/) or [pyproj](https://pypi.python.org/pypi/pyproj?). If one of these modules is available then it will be used to perfom all reprojection tasks.

Reprojection will be involved each time a coordinate or a dataset must be transformed to match the scene CRS. So, because the scene CRS leads all reprojection tasks, it must be carefully choosen to minimize transformation requests as much as possible. It's a good idea to harmonize your data to the same CRS through a dedicated software like QGIS before trying to import them in Blender.


- **For developpers**

The *GeoScene* class is a simple Python interface to manage custom scene properties. Using this class instead of directly setting the property is easier and offers more control (input validation, update triggers ...).

The georef manager panel is building as a reusuable layout that can be easily append to another addon layout.

The *geoscene* addon register a set of operators to perform common usefull tasks to manage georef informations.

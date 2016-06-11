## Custom properties

For storing georeferencing informations, BlenderGIS creates some custom properties in the scene.

- **Spatial Reference System (SRS)**

A map is commonly building through a cartographic projection witch transform angular coordinates on earth surface to planar coordinates and allows the representation of a territory that minimize distoritions or preserve some properties.

It's essential to know whats the SRS using to store and represent the geodata you want to use, because mixing data in differente SRS is not possible without reprojection capabilities.

The Spatial Reference Identifier (SRID) is an unique value used to unambiguously identify a coordinate reference system. SRID is in the form AUTHORITY:CODE but most of the time authory just refer to EPSG because the large majority of commonly used SRS are defined in the widely used EPSG database


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_srid.jpg)

- **Scene origin geolocation**

Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64). That's why it's necessary to create the mesh near to the scene origin.

For avoid georeferencing lost, custom properties are used to keep track of scene origin coordinates.

The most universal way to store the geolocation of a point is as angular coordinates : longitude and latitude.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_lonlat.jpg)

However, refering to longitude and latitude is not enough, we need to know what's the map projection and to be able to convert from angulars coordinates to this projected system (and vice versa) which involve reprojection capabilities through complex formulas and external software. That's why storing the scene origin coordinates directly in it's map projection system can be a better choice.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_xy.jpg)

BlenderGIS manage in priority the SRS coordinates of scene origin and update the corresponding longitude latitude if it can to do the math. Maintening angular coordinates up to date is useful to ensure compatibility with orthers addons witch prefers storing scene origin as longitude latitude.

- **Map scale denominator**


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_sk_scale.jpg)


## Geoscene addon


Theses properties can be managed through the geoscene addon which provides a panel showing current georeferencing informations and useful operators.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel.jpg)


- **Predefinate CRS**


Geoscene addon offers the possibility to define, save and manage a set of predefined Coordinate Reference System (CRS). 

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpg)

Adding a new predefined CRS can be an easy task thanks http://epsg.io/ service it's possible to perfom a simple keyword search.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpg)


- **Georef manager**

It's possible to switch the scene CRS

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)


A scene is considered correctly georeferenced when at least a valid CRS is defined and the coordinates of scene's origin in this CRS space is set. On the other hand a geoscene will be broken if the origin is set but not the CRS.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpg)

Furthermore, if the origin is only set as longitude/latitude the geoscene still remains broken. However, there is a dedicated operator to update projected coordinates from angulars coordinate sand vice versa.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin2.jpg)


- **Reprojection capabilities**

built in functions

epsg.io

proj4 interface : gdal osr or pyproj


- **For developpers**

GeoScene class

reusable layout

operators

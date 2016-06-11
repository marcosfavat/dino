For storing georeferencing informations, BlenderGIS creates some custom properties in the scene.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_idprops.jpg)

- **Spatial Reference System (SRS)**

A map is commonly building through a cartographic projection witch transform angular coordinates on earth surface to planar coordinates and allows the representation of a territory that minimize distoritions or preserve some properties.

It's assential to know whats the SRS using to store and represent the geodata you want to use, because mixing data in differente SRS is not possible without reprojection.

The Spatial Reference Identifier (SRID) is an unique value used to unambiguously identify a coordinate reference system. SRID is in the form AUTHORITY:CODE but most of the time authory just refer to EPSG because the large majority of commonly used SRS are defined in the widely used EPSG database


- **Scene origin geolocation**

Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64). That's why it's necessary to create the mesh near to the scene origin.

For avoid georeferencing lost, custom properties are used to keep track of scene origin coordinates.

The most universal way to store the geolocation of a point is as angular coordinates : longitude and latitude.

However, refering to longitude and latitude is not enough, we need to know what's the map projection and to be able to convert from angulars coordinates to this projeted system (and vice versa) which involve reprojection capabilities through complex formulas and external software.

That's why storing the scene origin coordinates directly in it's map projection system can be a better choice.



**Geoscene addon**


Theses properties can be managed through the geoscene addon.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpg)


wiki in progress ...

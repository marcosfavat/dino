Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64). That's why it's necessary to create the mesh near to the scene origin.

For avoid georeferencing lost, BlenderGIS creates some custom properties to the scene.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_idprops.jpg)

Theses properties can be managed through the geoscene addon.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpg)


wiki in progress ...

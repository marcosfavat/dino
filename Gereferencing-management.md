Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64). That's why it's necessary to create the mesh near to the scene origin.

For avoid georeferencing lost, BlenderGIS creates some custom properties to the scene.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_idprops.jpeg)

Theses properties can be managed through the geoscene addon.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_panel.jpeg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_prefs.jpeg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_set_crs.jpeg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_add_predef_crs.jpeg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_link_origin.jpeg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/geoscene_broken.jpeg)


wiki in progress ...

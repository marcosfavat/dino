Blender (and most of 3d software) cannot strongly handle objects that are far away scene origin. Furthermore, Blender works with coordinates as single precision (float32). The single float value actually has about [7 significant digits of precision](http://en.wikipedia.org/wiki/Floating_point#Internal_representation). On the other hand, geographic data is stored across a projection system (generally in meters) that gives high coordinates values. Projected coordinates must be represented as double precision (float64).

That's why it's necessary to create the mesh near to the scene origin. For avoid georeferencing lost, when you import a shapefile or a georaster, the script creates custom properties to the scene. Theses properties represent the shift values operate in X and Y axis.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/custom_props.jpeg)

When you try to import a shapefile or a georaster, if the scene already contains these custom properties, you will have the opportunity to use them to adjust the position of the new imported object.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/custom_props_considere.jpeg)

**The overlay will be correct only if the geographic projection system is the same.** Note that one Blender unit = one map coordinates system unit. So, units depend on your data.
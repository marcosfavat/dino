Starting working with geodata from scratch

1) Delete all object and save the blend file

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/1_delete.jpg)


2) Install BlenderGIS addon and set the cache folder in preferences settings

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/2_cache_folder.jpg)

3) Start *basemap* with `*` key, an option dialog appears for setting up the map source

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/3_basemap.jpg)

Press ok for start the map viewer, after few seconds the world map will be displayed

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/4_world_map.jpg)

Use your your mouse wheel to pan (`wheel click`) or zoom the map (`wheel scroll`). You can also zoom to a drawing region by pressing `B`, or search for a specific location to zoom to by pressing `G`. You can switch layer source by pressing `space bar` or access to several options by pressing `o`. Press `echap` key to exit map viewer navigation.

Note : The map is displayed as background image in the 3d view. You can edit the background image setup in the properties panel of the 3d view.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/5_bkg_image.jpg)


4) In the map viewer navigation mode, when the map location and zoom is correct, press `E` key to export the current map view to a new textured plane mesh

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/6_exported_plane_mesh.jpg)

Sometime the resolution of the image for the desired area is too low, fortunatly it's possible to force basemap to download more detailed zoom level while maintaning the actual extent view. To do this, when basemaps is running and the map view fixed to the desired extent and zoom level, just press `L` key. A red *zLock* label will appears to the bottom right of the 3d view. Now, when zooming, the extent area will be maintained as it but the addon will download tiles from highest zoom level increasing the map resolution.

You can also zoom while pressing `CTRL` key to just zoom over the generated map image without trigger new download and check in detail the resulting resolution. Again, when you're happy with the resulting image, press `E` to export it to a new plane mesh.


5) Next step consist of getting some relief from STRM data (global digital elevation model) using OpenTopograhy web service. With the plane mesh selected press *Get SRTM* button.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/10_get_srtm_button.jpg)

After few seconds, the plane will be wrap according to relief data.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/10_srtm_result.jpg)


6) Now we'll gather some 3d buildings from Open Street Map data and place them on the ground mesh. Switch the 3d view to top orthographic view and move to the correct extent that cover the desired data, then press *Get OSM* button in *GIS* tool tab.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/7_get_osm_button.jpg)

An options dialog will appears :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/8_get_osm_options.jpg)

Select *Ways*, *Buildings* and choose a default height value for extruding buildings that don't have any height information. This default height value can also be randomized between a threshold to add some realism. Check the option *Elevation from object* and select the mesh representing the ground relief, then press ok. After few seconds you will see the imported buildings.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/15_drop_result.jpg)

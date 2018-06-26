Starting working with geodata from scratch

1) Delete all object and save the blend file

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/1 delete.jpg)


2) Install BlenderGIS addon and set the cache folder in preferences settings

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/2 cache folder.jpg)

3) Start *basemap* with `*` key, an option dialog appears for setting up the map source

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/3 basemap.jpg)

Press ok for start the map viewer, after few seconds the world map will be displayed

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/4 world map.jpg)

Use your your mouse wheel to pan (`wheel click`) or zoom the map (`wheel scroll`). You can also zoom to a drawing region by pressing `B`, or search for a specific location to zoom to by pressing `G`. You can switch layer source by pressing `space bar` or access to several options by pressing `o`. Press `echap` key to exit map viewer navigation.

Note : The map is displayed as background image in the 3d view. You can edit the background image setup in the properties panel of the 3d view.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/5 bkg image.jpg)


 4) In the map viewer navigation mode, when the map location and zoom is correct, press `E` key to export the current map view to a new textured plane mesh

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/6 exported plane mesh.jpg)

Sometime the resolution of the image for the desired area is too low, fortunatly it's possible to force basemap to download more detailed zoom level while maintaning the actual extent view. To do this, when basemaps is running and the map view fixed to the desired extent and zoom level, just press `L` key. A red *zLock* label will appears to the bottom right of the 3d view. Now, when zooming, the extent area will be maintained as it but the addon will download tiles form highest zoom level increasing the map resolution.

You can also zoom while pressing `CTRL` key to just zoom over the generated map image without trigger new download and check in detail the resulting resolution. Again, when you're happy with the resulting image, press `E` to export it to a new plane mesh.


5) Now we'll gather some 3d buildings from Open Street Map data. With the new plane mesh selected, press *Get OSM* button in *GIS* tool tab.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/7 get osm button.jpg)

An options dialog will appears :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/8 get osm options.jpg)

Select *Ways*, *Buildings* and choose a default height value for extrude buildings that don't have any height information. This default height value can also be randomized between a threshold to add some realism. Check the option *Separate objects* and then press ok. After few seconds you will see the imported buildings.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/9 osm result.jpg)


6) Next step consist of getting some relief from STRM data (global digital elevation model) using OpenTopograhy web service. With the plane mesh selected press *Get SRTM* button.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/10 get srtm button.jpg)

After few seconds, the plane will be wrap according to relief data.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/10 srtm result.jpg)

7) For the final step, we need to drop our buildings to the relief. Since Blender 2.79, there is a drop to ground operator available with the *add advanced objects* addon. You need to activate the addon in blender preferences:

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/11 advanced object panel.jpg)

The tool buttons will appears in the *create* tab :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/12 drop toolbox.jpg)

Before performing the drop, we need to place the buildings above the relief mesh.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/13 drop before.jpg)

Then, with all buildings selected and relief as active object, press *drop selected* button. Operator options will appears on the bottom left panel : uncheck *Align to ground*

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/14 drop options.jpg)

Final result :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/quick_start/15 drop result.jpg)

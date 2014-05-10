**Worldfile**

The world file extension can be *.wld or must be respect one of these conventions: 

Image extension     |   World file extension
--------------------|-----------------------------------
tif                 |   tfw / tfwx / tifw
jpg                 |   jgw / jgwx / jpgw
bmp                 |   bpw / bpwx / bmpw
png                 |   pgw / pgwx / pngw

If the raster world file has rotation parameter you can still correctly import it on a plane or on a mesh but not as background.

**Import on a plane**

![](https://github.com/domlysz/BlenderGIS/raw/master/images/georaster_Mode_On_plane.jpeg)

**Import as background image**

![](https://github.com/domlysz/BlenderGIS/raw/master/images/georaster_Mode_As_Background.jpeg)

**Import on a mesh**

![](https://github.com/domlysz/BlenderGIS/raw/master/images/georaster_Mode_On_Mesh.jpeg)

**Troubles**

* If the imported image appeared fully black, try to config. the light according to the scene (for example try the sun light type)

* Because the scene can be very large, don’t forget to configure camera clipping distance according to the scene. If you still see black faces error after setting clip end distance try to set the clip start distance closer to the scene, it will help Blender to improve vertex position according to the Z depth of the camera.


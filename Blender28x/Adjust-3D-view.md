When importing a shapefile or a georaster, BlenderGIS will trying to adjust 3d view according to the imported mesh size. This is especially useful because geographic data can be very large while default 3d view settings are not suitable for such scales.

This adjustement consists to setup the 3D view's clip distances. This property is localized in the 3d view numeric panel.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/3dView_clip_dist.jpg)

In the same way you also need to configure camera clipping distance according to the scene. If you still see black faces error on render image after setting clip end distance try to set the clip start distance closer to the scene, it will help Blender to improve vertex position according to the Z depth of the camera.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender28x/images/camera_clip_dist.jpg)

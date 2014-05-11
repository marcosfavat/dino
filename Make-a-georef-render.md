If you have a georeferenced model, the panel will be active in the tool shelf GIS tab.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_tool_panel.jpg)

Choose the correct georef object that represents your map and then just click on the button to get a new camera with the good parameters.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_example.jpg)

**Tools options**  
You can name the camera and choose the target pixel size in map unit.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_redo_options.jpg)

In this example the mesh dimension on x axis is 3455 meters:

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_mesh_dimensions.jpg)

If the target pixel size for the render is set to 5 meters / px, render resolution will be 3455 / 5 = 691 px. Set up the target size automatically sets the render size accordingly.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_resolution.jpg)

The camera is set to ortho with the correct scale and location to enclose the mesh.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_cam_settings.jpg)

The script also try to set best Z location and clipping distance.

If you open a text editor and browse the loaded files, you will find the wordlfile that contains the georeferecing data.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_worldfile.jpg)

Now you can hit F12 and save the render output and the worldfile text on your disk. Don’t forget to name them correctly and accordingly.

Open them in your GIS software:

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/georender_result.jpg)
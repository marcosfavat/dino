This tool can import in Blender most of shapefile feature type : point, pointZ, polyline, polylineZ, polygon, polygonZ. But actually it cannot import multipoint, multipointZ, pointM, polylineM, polygonM and multipatch.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/shp_import_options.jpg)


**Troubles**

* This tool depends on pyshp library that is in beta version, so sometimes it cannot process the shapefile. Typically, if you got "Unable to read shapefile", "Unable to extract geometry" or "Unable to read DBF table" error, these are pyShp issues. In this case:

    * Try to check if there is any update of [pyshp lib](http://code.google.com/p/pyshp/downloads/list).

    * If there is no update available or if update doesn't correct the problem, try to open and re-export the shapefile with any GIS software. You can also try to clean/repair geometry, delete unnecessary fields...

* For polygons import, if you see faces which seem to be strangely filled try to remove duplicate vertex on the mesh (modify tolerance distance if necessary)

* The script can handle multipart geometry but actually if the part defines a polygon hole, a face will still be created.

* Because the scene can be very large, don’t forget to configure camera clipping distance according to the scene. If you still see black faces error on render image after setting clip end distance try to set the clip start distance closer to the scene, it will help Blender to improve vertex position according to the Z depth of the camera.

**How to import a shape file with the right projection**

Step 1: go to your user preferences -> addons -> search for "geoscene" and look to the properties. With the plus, add the crs you need to project your file (can be found in the .prj file near your .shp file or you can ask the person who created the shape file or try the different standards specific to the area of your project).

![go to user prefs to add a crs](https://cloud.githubusercontent.com/assets/12851284/16179399/c358e166-3664-11e6-9d8f-4c503e2f064a.png)

When you know the code or part of the name, their is a search function to find the exact CRS and add it with it's description already set.

![use the search function](https://cloud.githubusercontent.com/assets/5639024/16125633/d2f35c36-33f4-11e6-83d1-b4e9aa5c14b6.jpg)

Step 2: set the scene crs in the blender-GIS Tab of your 3D-View toolshelf.

![](https://cloud.githubusercontent.com/assets/5639024/16125647/dd0f5a76-33f4-11e6-85be-48387ccffb9b.jpg)
![](https://cloud.githubusercontent.com/assets/5639024/16125648/dd12a5b4-33f4-11e6-9572-d8324f66d2e2.jpg)

Step 3: import the .shp (File->Import)

![](https://cloud.githubusercontent.com/assets/5639024/16125660/e8361e62-33f4-11e6-92c3-cc98a51ac300.jpg)

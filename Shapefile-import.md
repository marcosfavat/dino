**Extrusion**

You need to know & manually enter the name of the field that contains the values (don't worry about case sensitive). Note that the extrusion can be very slow with lot of features but you can see progress output in Blender console.

**Troubles**

This tool depends on pyshp library that is in beta version, so sometimes it cannot process the shapefile. Typically, if you got "Unable to read shapefile", "Unable to extract geometry" or "Unable to read DBF table" error, these are pyShp issues. In this case:

1. Try to check if there is any update of [pyshp lib](http://code.google.com/p/pyshp/downloads/list).

2. If there is no update available or if update doesn't correct the problem, try to open and re-export the shapefile with any GIS software. You can also try to clean/repair geometry, delete unnecessary fields...

For polygons import, if you see faces which seem to be strangely filled try to remove duplicate vertex on the mesh (modify tolerance distance if necessary)
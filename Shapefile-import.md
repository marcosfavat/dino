Troubles:

This tool depends on pyshp library that is in beta version, so sometimes it cannot process the shapefile. Typically, if you got "Unable to read shapefile", "Unable to extract geometry" or "Unable to read DBF table" error, these are pyShp issues. In this case:

1. Try to check if there is any update of [pyshp lib](http://code.google.com/p/pyshp/downloads/list).

2. If there is no update available or if update doesn't correct the problem, try to open and re-export the shapefile with any GIS software. You can also try to clean/repair geometry, delete unnecessary fields...
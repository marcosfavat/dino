
Warnings:
- This tool is still in developement and can be buggy or unstable
- Remember that service in Web Mercator projection do not give reliable distance measurement and are not suitable for precision modelling, use a local projection instead.
- It depends optionnaly on GDAL for reprojection support.


Navigation:
- Toogle map view : button in panel or `numpad asterix`
- Exit map view : `echap`
- Switch layer : `spacebar`
- Search function : `G` (go to)
- Edit options : `O`
- Export current map to a new textured plane : `E`
- Zoom map : `mousewheel` or `numpad+` and `numpad-`
- Pan map : `left click & drag` or `wheel click & drag` or `numpad 2,4,8,6`
- Zoom map to drawing box : `B`
- Zoom 3d view : `ctrl mousewheel` or `ctrl numpad+` and `ctrl numpad-`
- Pan 3d view : `ctrl left click & drag` or `ctrl wheel click & drag` or `numpad 2,4,8,6`
- Change scale : `alt mousewheel` or `alt numpad+` and `alt numpad-`


You can add your own service (WMS, WMTS, TMS) by adding its definition in a json like syntax directly in the file servicesDefs.py. You can also define your own custom tile matrix. 

Reprojection support :
- It's possible to seed on the fly a cache in local projection from a source in global projection like Web Mercator.
- It's also possible to keep the cache in Web Mercator and just reproject the final image to match the scene CRS

Reprojection is essential to work with an acceptable precision when consume service in Web Mercator.

Downloaded tiles are stored in an SQLite cache (Geopackage) for speed up upcoming request.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/basemaps_demo.gif)

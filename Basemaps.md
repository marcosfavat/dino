
Warnings:
- This tool is still in developement and can be buggy or unstable
- ~~For now, georef infos are not compatible with others BlenderGIS tools~~
- Remember that service in Web Mercator projection do not give reliable distance measurement and are not suitable for precision modelling, use a local projection instead.
- It depends on [Pillow](https://pypi.python.org/pypi/Pillow/3.2.0) and optionnaly on GDAL for reprojection support.
On Windows use the following commands to install Pillow:
`blender_install_folder\2.7x\python\bin\python.exe -m ensurepip`
`blender_install_folder\2.7x\python\bin\python.exe -m pip install pillow`


Navigation:
- Toogle map view : button in panel or `numpad asterix`
- Exit map view : `echap`
- Switch layer : `spacebar`
- Search function : `G` (go to)
- Edit options : `O`
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

Road map / todo:
- More tests and optimizations
- Better UI with some sort of layers manager : toogle source on the fly, display and overlay several sources in the same time ...
- ~~Harmonize scene georeferencing of others BlenderGIS tools to this one. Ensure also compatibility with dxf import/export and BlenderGeo.~~

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/basemaps_demo.gif)

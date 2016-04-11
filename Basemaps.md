
Warnings:
- This tool is still in developement and can be buggy or unstable
- Georef infos are not compatible with others BlenderGIS tools
- Service in Web Mercator projection do not give reliable distance measurement and are not suitable for precision modelling.
- It depends on ![Pillow](https://pypi.python.org/pypi/Pillow/3.2.0) and optionnaly on GDAL for support of others projections than web mercator.


Navigation (not yet fully implemented):
- toogle map view : button panel or numpad asterix
- exit map view : echap or enter
- zoom map : mousewheel or numpad + or numpad -
- pan map : left click & drag or wheel click and drag or numpad 2,4,8,6
- zoom 3dview : ctrl + mousewheel or ctrl + numpad + or numpad -
- pan 3dview : ctrl + left click and drag or ctrl + wheel click & drag or numpad 2,4,8,6
- change scale : alt + mousewheel or alt + numpad + or numpad -


You can add your own service (WMS, WMTS, TMS) by adding its definition in a json like syntax directly in the file servicesDefs.py. You can also define your own custom tile matrix.

Downloaded tiles are stored in an SQLite cache (Geopackage) for speed up upcoming request.


![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/basemaps_demo.gif)

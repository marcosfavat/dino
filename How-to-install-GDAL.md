[GDAL](http://gdal.org/) is a popular and powerful geospatial data processing library.

**Windows**

Core binary file can be downloaded from [gisinternals.com](http://www.gisinternals.com/sdk/). Scroll down to *release versions* table and click on the relevant link in the *Downloads* column (32 or 64 bit). From the new page download the GDAL Core file (gdal-[version]-[build]-core.msi)

Using binary files needs to edit environmental variables like this:

*todo: append screenshoot here*

Actually installing binary files is good enought to get the addon working as well. You can also use GDAL Python API but in this cas you need to install the binding.

Python binding is also available right here, but these versions aren't compiled accross Numpy. Without Numpy, the binding will not have all of its functionality and can not be used with the addon.

Fortunately other Python packages can be found [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#gdal). This distribution also includes GDAL binary files. If you already installed binary files you can delete them from Python folder (just delete *.exe and *.dll).

Installing Python binding from these setup files requires that Python exists on your computer. So the first step is to install Python (download it [here](https://www.python.org/downloads/)). Choose the version that corresponds to the version delivered with Blender.

GDAL Python binding installer creates a new folder named osgeo in *C:\Python33\Lib\site-packages*. Just copy osgeo folder in Python folder tree of Blender: *C:\Program Files\Blender Foundation\Blender\2.70\python\lib\site-packages*

Note that Numpy version uses to compile GDAL binding needs to match the version ship with Blender.

To test the install open Blender Python console and type:

`from osgeo import gdal`

`from osgeo import gdalnumeric`

These statements should not return error.
[GDAL](http://gdal.org/) is a popular and powerful geospatial data processing library. GDAL is available as a set of commandline utilities (ready to use binaries files). The developer oriented library is available as a C/C++ API. Bindings in other languages, including Python, are also available.

**GDAL is an optional dependency**, most of the functionalities of BlenderGIS are available without it. If the addon does not works as expected, installing GDAL will not solve the issue. GDAL can be useful for advanced users who need more support for GIS specific fomats and reprojection tasks directly in Blender. However, if you want to deal with heterogeneous data formats, projections or extents, the most straightforward strategy is to preprocess your data with QGIS before trying the import into Blender. QGIS is a powerful open source desktop GIS software, this is an essential tool for working with BlenderGIS because it will help prepare the data for a smooth import. Futhermore, installing GDAL with Blender can be really tricky because Blender bundle it's how Python installation.

### Linux

GDAL binary and Python binding are available through ubuntugis repository

`sudo add-apt-repository ppa:ubuntugis-unstable`

`sudo apt-get install gdal-bin`

`sudo apt-get install python3-gdal`

`sudo apt-get install python3-numpy`

Install Blender from a repository instead of ready to use tarballs from blender.org.

`sudo add-apt-repository ppa:thomas-schiex/blender`

Installing through this way, Blender will use the version of Python existing on the system instead of it's own bundle version.

**Warning :** Currently, Numpy will fails if your distribution does not support Python 3.6. It can be solved by reinstalling Numpy with pip :

`sudo apt-get install python-pip python3-pip`

`sudo pip3 install -U numpy`

### Windows

On Windows, the most easiest way to install GDAL Python Binding is to use the packages build by Christoph Gohlke and available [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#gdal). Choose the package that match the version of Python bundle with Blender, you can determine it by opening the Python console in Blender. In the following screenshoot this is Python 3.5.3, the corresponding package is named *GDAL-2.2.4-cp35-cp35m-win_amd64.whl*.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/python_version.jpg)

The \*.whl package file contains a stand alone GDAL installation including all needed files (binaries, libraries, Python binding...), so you don't need to install any other file.

Blender bundle it's own Python executable at `blender_install_folder\2.7x\python\bin\python.exe`, after downloading the whl file, put it in this directory and then open a new Windows terminal from this folder. To do this, in the file explorer right click while maintaining shift key and choose *open command window here*.

You need *pip* utility to install \*.whl package files, so the first step is to install *pip* with the following command :

`python.exe -m ensurepip`

Then you can install the wheel file:

`python.exe -m pip install GDAL-2.2.4-cp35-cp35m-win_amd64.whl`

GDAL will be installed into `blender_install_folder\2.7x\python\lib\site-packages\osgeo`

To finalize the installation, it's necessary to define a new Windows environment variable named *GDAL_DATA* and pointing the following directory : `blender_install_folder\2.7x\python\lib\site-packages\osgeo\data\gdal`

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gdal_data.jpg)


To test the install open Blender Python console and type:

`from osgeo import gdal`

`from osgeo import gdalnumeric`

These statements should not return error. If gdalnumeric import raise an error it's because Numpy version uses to compile GDAL binding doesn't match the version ship with Blender. So in this case just update Numpy with the [corresponding package](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy)

For testing if GDAL_DATA environment variable is correctly setup type :

`from osgeo import osr`

`osr.SpatialReference().ImportFromProj4('+init=epsg:3857')`

The second statement must return zero, a value >0 refers to an error code.


### Mac Osx

*Tested on Yosemite 10.10 and Blender 2.74*

1) Install Xcode and Macports from this link :
 https://www.macports.org/install.php

2) Install gdal and gdal python bindings
Open a terminal from spotlight or from Applications => Utilities => Terminal
Then type with administratives rights :

`sudo port install gdal py34-gdal`

3) Copy osgeo folder from python bindings to blender

`cp -rf /opt/local/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/site-packages/osgeo /**where_you_put_blender_on_your_mac**/Blender/blender.app/Contents/Resources/2.74/scripts/modules/`

Replace *where_you_put_blender_on_your_mac* with the path where you run or install Blender

Test it in Blender Python console like windows installation.

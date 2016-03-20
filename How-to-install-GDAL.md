[GDAL](http://gdal.org/) is a popular and powerful geospatial data processing library. GDAL is available as a set of commandline utilities (ready to use binaries files). The developer oriented library is available as a C/C++ API. Bindings in other languages, including Python, are also available.

**GDAL is an optional dependency**, all the functionalities of BlenderGIS are available without it. It will be used only if possible and only for georaster import with the *As DEM* option.

### Linux

GDAL binary and Python binding are available par ubuntugis repository

`sudo add-apt-repository ppa:ubuntugis-unstable`
`sudo apt-get install gdal-bin`
`sudo apt-get install python3-gdal`
`sudo apt-get install python3-numpy`

Install Blender from a repository instead of ready to use tarballs from blender.org.

`sudo add-apt-repository ppa:thomas-schiex/blender`

Installing through this way, Blender will use the version of Python existing one the system instead of it's own bundle version.


### Windows

On Windows, the most easiest way to install GDAL Python Binding is to use the packages available [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#gdal). Note that these distributions also includes GDAL binary files.

You need pip to install *.whl package files. The Python installation bundle with Blender do not include pip but include distutils. So it's possible to run [get-pip.py](https://bootstrap.pypa.io/get-pip.py) to install pip :

`blender_install_folder\2.7x\python\bin\python.exe get-pip.py`

And then install the wheel:

`blender_install_folder\2.7x\python\bin\python.exe -m pip install GDAL-2.0.2-cp34-none-win_amd64.whl`

To test the install open Blender Python console and type:

`from osgeo import gdal`

`from osgeo import gdalnumeric`

These statements should not return error. If gdalnumeric import raise an error it's because Numpy version uses to compile GDAL binding needs to match the version ship with Blender. So in this case just update Numpy with the [corresponding package](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy)


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

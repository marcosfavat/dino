*Please don't except a success story if you don't really know what you are trying to import in Blender... Use [QGIS](http://www.qgis.org), to explore your data beforehand.*

**Warning** : for Linux users who choose to install Blender through [`ppa:thomas-schiex/blender`](https://launchpad.net/~thomas-schiex/+archive/ubuntu/blender), Numpy will fails if your distribution does not support Python 3.6. It can be solved by reinstalling Numpy with pip : `sudo apt-get install python-pip python3-pip` and then `sudo pip3 install -U numpy`

**Install**

This addon require at least Blender v2.80 to work correctly (old code for Blender 2.79 is still available in the dedicated branch). It also optionally rely on [GDAL](https://github.com/domlysz/BlenderGIS/wiki/How-to-install-GDAL) for advanced features.

Download source archive from github.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/install_git_download.jpg)

Then open Blender User Preferences and use **Install from file** option to install the addon from downloaded zip. Don’t forget to enable the addon and save settings.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender27x/images/install_from_file.jpg)

**Usage**

All tools are available in a new dedicated *GIS* menu.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender28x/images/bgis_menu.jpg)

The geoscene manager panel is available from the 3d view properties panel.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender28x/images/geoscene_panel.jpg)

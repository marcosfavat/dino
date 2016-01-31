In node editor when a color ramp node is selected a new panel named Reclassify appear in editor properties sheft.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_panel.jpg)

The main purpose of the panel is to help the user to setting the color ramp stops. Color ramp node input values must be range from 0 to 1, so it's hard to make the realationship between theses normalized values and a physical value like height, slope or aspect.

Values display in reclassify panel are converted to represents their physical equivalent. To compute this correctly the user must choose the display mode of the panel according to the currently applied materials.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_mode.jpg)

* **Height** mode scale the values according to the object bounding box to get the true altitude
* **Slope** mode multiply the node value by 100 to get the slope in degrees (as explained in node setup description for slope material)
* **Aspect** mode multiply the value by 360 to get azimuth angle (with north = 0°)


**Quick color gradient edit**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_quick_gradient.jpg)

Description to do

**Use SVG gradient**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_svg_gradient.jpg)

This addon is packaged with a few SVG color ramp. All these ramp are pick up from the [cpt-city archive](http://soliton.vm.bytemark.co.uk/pub/cpt-city/). SVG files are stored in *Blender_install_folder\2.xx\scripts\addons\terrain_analysis\gradients*. You can add, edit or remove svg file from here to manage your color ramp library.

**Export to SVG**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_export_svg.jpg)

You can export actual color ramp node configuration to svg files. This file will be stored in *Blender_install_folder\2.xx\scripts\addons\terrain_analysis\gradients* folder, so the ramp is added to the library and can be immediatly reused.

**Auto reclass**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto.jpg)

Description to do

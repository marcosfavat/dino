In node editor when a color ramp node is selected a new panel named Reclassify appear in editor properties sheft.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_panel.jpg)

The main purpose of the panel is to help the user to setting the color ramp stops. Color ramp node input values must be range from 0 to 1, so it's hard to make the relationship between theses normalized values and a physical value like height, slope or aspect.

Values display in reclassify panel are converted to represents their physical equivalent. To compute this correctly the user must choose the display mode of the panel according to the currently applied materials.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_mode.jpg)

* **Height** mode scale the values according to the object bounding box to get the true altitude
* **Slope** mode multiply the node value by 100 to get the slope in degrees (as explained in node setup description for slope material)
* **Aspect** mode multiply the value by 360 to get azimuth angle (with north = 0°)

### **Manual editing**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_manual_edits.jpg)

You can directly edit in the panel color and position of each stops of the color ramp node. You can also add a new stop or delete and existing one.

### **Color gradient settings**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_reverse.jpg)

You can switch color ramp node interpolation between *constant* and *linear*. Linear interpolation make a continious ramp while constant make a discrete ramp.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_switch.jpg)

You can also reverse the color ramp. Note that this tool doesn't work like the tool include in the color ramp node because it reverse only the colors and not the positions

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_reversed.jpg)

#### **Quick color gradient edit**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_quick_gradient.jpg)

This tool allows to change colors of each stops of the color ramp node by refering to a small gradient defined on the fly by the user. This gradient defines at least 2 colors and up to 5.

The colors are displaying in the popup dialog and represents the expected colors at positions 0 - 0.2 - 0.4 - 0.6 - 0.8 - 1. The 3 intermediates colors are optionals, they'll be used only if the checkbox bellow them are enabled.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_quick_gradient_details.jpg)

For each stop of the color ramp node, the script evaluate the color inside the desired gradient at the stop position. For example, color at position 0.5 will be computed by interpolating between color 3 and color 4.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_quick_gradient_examples.jpg)

Sometimes, there is no stops at the bounds of the color ramp node (positions 0 and 1). To fit the quick gradient definition to this special case you can use the dedicated option.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_fit.jpg)

#### **Import SVG gradient**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_svg_gradient.jpg)

This addon is packaged with a few SVG color ramp. All these ramp are pick up from the [cpt-city archive](http://soliton.vm.bytemark.co.uk/pub/cpt-city/). SVG files are stored in *Blender_install_folder\2.xx\scripts\addons\terrain_analysis\gradients*. You can add, edit or remove svg file from here to manage your color ramp library.

Like previous tool, for each stop of the color ramp node, the script evaluate by interpolation the color inside the svg gradient at the corresponding stop position.

#### **Export to SVG**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_export_svg.jpg)

You can export actual color ramp node configuration to svg files. This file will be stored in *Blender_install_folder\2.xx\scripts\addons\terrain_analysis\gradients* folder, so the ramp is added to the library and can be immediatly reused.

There are 2 methods to build the svg file:
* **Use actual stops** build svg ramp with exactly the same positions and colors currently define in the color ramp node. There is no interpolation.
* **Interpolate n colors** produce a svg gradient with a predefined number of colors interpolate from the color ramp node definition. The interpolation options of the popup window will only be used along with this method.

SVG gradient can be continuous or discrete, use the dedicated checkbox to produce one or the other type.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_type.png)

#### **About color space and interpolation methods**

Interpolation can be computed through RGB or HSV color space. HSV interpolation often gives better results, but in this color space hue is cyclic and the interpolation must be done through the shortest path (clockwise or counterclockwise). By defaut this addon use the shortest path.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_hsv.png)

You can use several algorithms for interpolation:
* **Linear** is the most simple way but this method do not provides a smooth interpolation.
* **Spline** interpolation gives smooth results. Here we use the Akima method instead of the well know Cubic spline. The disadvantage of cubic splines is that they could oscillate in the neighborhood of an outlier while the Akima spline is less affected by them.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_interpo_graph.png)
* **Discrete** isn't an interpolation method, it just return the previous color.
* **Nearest** isn't an interpolation method, it just return the nearest color.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/gradient_interpo_nearest.png)

### **Auto reclassify**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto.jpg)

This tool allows to automatically classify the values following specified rules:
* **Fixed classes number** produce an predefined number of classes by divided equally the entire range of data values. The interval is determined by the desired number of classes. Note that for define x classes we need x+1 stops in the color ramp.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto_classes.jpg)
* **Equal interval value** produce a similar result but instead of predefining the number of classes, we define the interval. The number of classes is determined by the desired interval.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto_interval.jpg)
* **Target interval value** make a stop for each multiple of the target value. This method is ideal if you want to classifying with an *absolute step* value. The intervals will not be necessary equals.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto_target.jpg)
* **Aspect reclassification** is a specific method dedicated to aspect map. The number of classes determine the number of azimuth represented.
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_reclassify_auto_aspect.jpg)

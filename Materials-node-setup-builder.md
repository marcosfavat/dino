This tool build material nodes setup for Cycles designed to help analysis hieght, slope and aspect of a tarrain with color gradient.

Operator is accessible from 3D view tools sheft.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_build_nodes_setup.jpg)

When launched it build three new materials and add a new material slot to the active object. You can quickly change material by assign a new one to this slot.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_switch_material.jpg)

**Height map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_node_setup.jpg)

This node setup is specific to the object on which the material is applied because it depends on the bounding box of the object and there is no node to get bounding box attribute of an object.

To get Z value of the mesh we use the *position* attribute of the *geometry* node, witch provide object coordinates in world space. The values must be normalize between 0 and 1 before connecting the color ramp node. A node group is used to normalize Z coordinates with the standard formula:
`outValue = (inValue - inMin) * (outMax - outMin) / (inMax - inMin) + outMin`
Where inMin and inMax represents zMin and zMax
When normalize between 0 to 1, we get:
`outValue = (inValue - inMin) * (1 - 0) / (inMax - inMin) + 0`
`outValue = (inValue - inMin) / (inMax - inMin)`

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_node_group.jpg)

**Slope map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_slope_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_slope_map_node_setup.jpg)

Description to do

**Aspect map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_aspect_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_aspect_map_node_setup.jpg)

Description to do

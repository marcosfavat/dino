This tool build material nodes setup for Cycles designed to help analysis hieght, slope and aspect of a tarrain with color gradient.

Operator is accessible from 3D view tools sheft.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_build_nodes_setup.jpg)

When launched it build three new materials and add a new material slot to the active object. You can quickly change material by assign a new one to this slot.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_switch_material.jpg)

**Height map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_node_setup.jpg)

This node setup is specific to the object on which the material is applied because it depends on the bounding box of the object and currently there is no node to get bounding box attribute of an object. So, the script add 2 *Value* nodes for specify zmin and zmax properties.

To get Z values of the mesh we use the *Position* attribute of the *Geometry* node, witch provide object coordinates in world space. *Separate XYZ* node is used to extract Z component of the vector.

These values must be normalize between 0 and 1 before connecting the color ramp node. A node group is used to normalize Z coordinates with the standard formula:

`outValue = (inValue - inMin) * (outMax - outMin) / (inMax - inMin) + outMin`

Where inMin and inMax represents zMin and zMax.

When normalize between 0 to 1, we get:

`outValue = (inValue - inMin) * (1 - 0) / (inMax - inMin) + 0`

`outValue = (inValue - inMin) / (inMax - inMin)`

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_height_map_node_group.jpg)

Note that if `inMin = 0` then `outValue = inValue / inMax`, it's the formula we'll use to normalize angle values in Slope and Aspect material node setup.

**Slope map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_slope_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_slope_map_node_setup.jpg)

Slope is the angle between face normal vector and Z axis vector. From linear algebra we know that the dot product of 2 vectors equals to cos(alpha) where alpha is the angle between these vectors.

**`Slope = arccos(N.Z)`**

Computing the dot product between normal and z axis is equivalent to extract Z component of the normal vector
`N.Z = (x,y,z).(0,0,1) = Z`

*Geometry* node provides normal vector in world space and *Separate XYZ* node is used to extract Z component of the vector. Then we compute arc-cosine and convert radians to degrees by multiplying by 180/pi.

Angles must be normalized to get values range from 0 to 1 before connecting color ramp node. The values returning by arc-cosine are range from 0 to 180°, but the slope of a terrain will never exceeds 90° (vertical cliff). So it's more convenient to normalize values by 100° because in this case we can easily link a slope value to it's color ramp position, for example a position of 0.5 in the color ramp node corresponds to a slope of 50°.

**Aspect map**

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_aspect_map_example.jpg)
![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_aspect_map_node_setup.jpg)

Computing azimuth can be summarized to a 2D problem by taking face normal vector and project it on XY plane.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_azimuth_trigo.png)

**`aspect = atan(x/y)`**

*Geometry* node provides normal vector in world space and projection is obtained by setting Z component to zero. Then we compute arc-tangent and convert radians to degrees by multiplying by 180/pi.

Azimuth angle must be corrected according to the quadrant where the tangent is computed. This correction can be obtained by following 2 simples rules :
* Add 180° if y is negative
* Add 360° if x positive and y positive

Finally angle must be normalized by 360° to get values range from 0 to 1 before connecting color ramp node.

Also, flat angle is a special case that must be considered separately. Here we use a mix shader to define a specific color to flat area.

**Overlay**

You can use mixRGB node to overlay aerial photography or topographic map a terrain analysis.

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/analysis_overlay.jpg)

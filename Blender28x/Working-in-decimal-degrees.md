All import/export tools provide an option named *Angular coords*

If your data is stored in a geographic coordinate system in degrees like WGS84 you can tick *Angular coords* option to convert them to meters.

The conversion is realized with an equirectangular projection because it's the simplest way to convert geo coords in cartesian world. Equirectangular projection is also called "non-projection" because the horizontal coordinate is simply longitude, and the vertical coordinate is simply latitude, with no complex transformation applied. 

To compute distance in meters of one degree, the script just divide earth perimeter at equator by 360, giving about 111 meters.

But the disadvantage of this projection is that horizontal distortion increases as the distance from the equator increases. You really may consider working with projected data.

When the scene is georeferenced, for example using *basemaps* addon, it's possible to directly request for OSM data :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_demo.gif)


But it's also possible to import an xml file :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_import_file.jpg)


In this case, if the scene is not georeferenced then data will be reprojected into the right UTM zone.



Importer allows to filter features by type (node, way or area) and by tags :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_op_props.jpg)


It's possible to edit the list of filter tags available by default

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_tags_prefs.jpg)



Standard import will create one mesh for each feature type and filter tag combinaison :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_outliner.jpg)


These meshes contains vertex group to retrieve features names, tags and relations :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_vertex_groups.jpg)

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_vertex_group_select.jpg)


It's also possible to sperate each feature into distinct objects, but keep in mind that Blender is not designed to handle hundreds of objects...

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_outliner_separate.jpg)


In this case, relations will be transpose into groups :

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/images/osm_relations_groups.jpg)

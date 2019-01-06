The shapefile exporter tool can be used to produce 3d shapefile from mesh data. The expected shape type (point, line polygon) must be defined by the user.

There are 2 different export modes:

- **Single object** : each faces, lines or points of the mesh will be exported as new shapefile feature.
- **Collection** : this mode allows to export a batch of objects stored in a collection. Each object will be exported as new shapefile feature, so if an object contains more than one face, line or point then multipart features will be produced. If an object has custom properties, then they will be transposed in the shapefile's attributes table

![](https://raw.githubusercontent.com/wiki/domlysz/blenderGIS/Blender28x/images/shp_export_options.jpg)

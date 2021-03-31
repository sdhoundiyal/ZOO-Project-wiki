## Exercise

\_\_TOC\_\_ \[/ZOO-Project/ZOO-Project/wiki/ZooWorkshop/FOSS4GJapan
WorkShop table of content\]

You know everything now about writting zcfg matadata files and get short
pieces of code in `service.c` or `ogr_service_provider.py` depending if
you choosen C or Python programming language respectively.

The goal of this exercise is to implement the following multiple
geometries services :

-   Intersection
-   Union
-   Difference
-   SymDifference

### C version {#c_version}

Your are now invited to edit the `source.c` file you have created during
this workshop to add the multiple geometries, using the following OGR
C-API functions :

-   [OGR_G\_Intersection](http://www.gdal.org/ogr/ogr__api_8h.html#5a271b5c7b72994120e7a6bbc7e7e5cb)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_Union](http://www.gdal.org/ogr/ogr__api_8h.html#f58f2cfbdb2497659d2eabea73d3b8a0)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_Difference](http://www.gdal.org/ogr/ogr__api_8h.html#497977bec6ecd9dade7a9694f776be64)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_SymmetricDifference](http://www.gdal.org/ogr/ogr__api_8h.html#d6dacf495617a230c6f19950bc415f17)(OGRGeometryH,
    OGRGeometryH)

You can use the `Boundary.zcfg` file as example, rename the
`InputPolygon` input to `InputEntity1` and add a similar input named
`IntputEntity2`. You are invited to update other values in the ZOO
Metadata File to set the proper metadata informations.

### Python Version {#python_version}

Your are invited to edit the `ogr_ws_service_provider.py` file you
created during this workshop to add the multiple geometries using the
following `osgeo.ogr` `Geometry` methods applied on the first `Geometry`
instance :

-   Intersection(Geometry)
-   Union(Geometry)
-   Difference(Geometry)
-   SymmetricDifference(Geometry)

You can once again use the `Boundary.zcfg` file as example, rename the
`InputPolygon` input to `InputEntity1` and add a similar input named
`IntputEntity2`. You are invited to update other values in the ZOO
metadata file to set the proper metadata informations.

### Testing your services {#testing_your_services}

Once the multiple geometries Services are deployed on your local
environment, please reload the `zoo-ogr.html` file created during the
previous section from your browser and test your brand new ZOO
Services.\
\[/ZOO-Project/ZOO-Project/wiki/ZooWorkshop/FOSS4GJapan WorkShop table
of content\]

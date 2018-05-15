## gdalinfo to dump geotiff information

This command dumps all the geographic information in the file (bounding box, channels, etc)

    gdalinfo myfile.tif

## Select subset of geotiff preserving geo information

```
# Get the dimensions of the tiff from metadata
gdalinfo source.tif | head

# cut tiff. Args are xoffset yoffset xlength ylength (origin is top-left corner)
gdal_translate -srcwin 500 500 1000 1000 source.tif slice.tif

# compare geo information of the original and new tiff
gdalinfo source.tif | tail
gdalinfo slice.tif | tail
``` 

## gdal_translate

Change image from geotiff to png:

    gdal_translate input.tif output.png -of png
    
## ogr2ogr- Dump information from shapefile

```
INPUT=my_shapefile.shp
OUTPUT=shape_as_wkt.csv
ogr2ogr -f CSV ${OUTPUT} ${INPUT} -lco GEOMETRY=AS_WKT
cat ${OUTPUT}
```

## Other gdal tools:

* gdal_translate
* gdaladdo
* gdalwarp
* gdal_merge.py
* gdaltindex

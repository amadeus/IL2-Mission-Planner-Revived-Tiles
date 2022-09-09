# Il-2 Tiles Service

Providing map tiles for [IL2 Mission Planner Revived](https://serverror.github.io/IL2-Mission-Planner/).

## Using gdal2tiles.py

Run the python script as follows:

`gdal2tiles.py [STITCHED MAP PNG] -z 0-7 -p raster -l`

Adjust number of zoom levels as necessary.

## Using dds_to_png.sh

Copy shell script to directory containing dds files. Run to convert all dds files within. Repeat for other folders.

## Stitching

Imagemagick's "montage" is the easiest way to stitch together the tiles. Use it as follows:

`montage *.png -mode Concatenate -tile 20x stitch.png`

Adjust tile number based on the number of image tiles in one row.

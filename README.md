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

## To get this properly working, you must first setup python virtual env, then
do:

### Requirements
```
# ideally 3.9 or whatever version matches in requirements.txt
# Pretty sure they need to match or else the bindings will be fucked
brew install gdal
brew install pyenv pyenv-virtualenv
```

Once deps are installed, you'll need to `cd` into the project directory to
enable direnv to take over. You may need to manually install the apropriate
python version in pyenv (see the commented out line in `.envrc`).

Then when you cd into the directory it should activate the proper virtual env,
and if it's your first time, you'll need to run

```
pip install -r requirements.txt
```

to ensure the proper local deps are installed. **NOTE:** Pretty sure the
locally installed gdal and globally installed gdal may need to match.  Because
Homebrew sucks, you may need to just update the requirement.txt version in
order for them to match.

If you have to upgrade gdal, then you're going to need to probably update the
gdal2tiles.py file, you can locate it using the following command:

```
find $(python -c "import site; print(site.getsitepackages()[0])") -name "gdal2tiles.py"
```

Then copy it over and overwrite the existing gdal2tiles.py file in this repo

### Create Tiles

```
python ./bin/gdal2tiles.py ./src/stalingrad_ftc/stalingrad_ftc.png dist/stalingrad_ftc -z 0-6 -p raster --xyz
```

Things to look out for -- make sure you match zoom levels to the original map.

May be worth modifying the max zoom to 6 or 7 depending on the map.  If you're
matching an existing map, then it's probably worth matching the max zoom
directory there as well.

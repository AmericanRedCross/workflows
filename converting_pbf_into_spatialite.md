Converting osm.pbf (Geofabrik) files into spatialite databases
===========================================

PBF files take up less space than other data formats, so they're quicker to download. Here's how to convert them into spatialite databases, which are what most of our QGIS map styles are based on.

## Setup

1. Make you have GDAL installed.
2. Download a PBF file for the area you are looking for from Geofabrik: http://download.geofabrik.de/, HOT Export Tool: http://export.hotosm.org, or other source (e.g. activation wiki)
3. Put the download somewhere accessible (suggestion: set up a consistent folder for all OSM extracts)
4. Place your PBF file inside the folder. The file from Geofabrik will download with an `.osm.pbf` extension. Manually change the text of the filename to delete the `.osm` part and just end with `.pbf`. Example: Download.osm.pbf -> Download.pbf
5. Geofabrik normally gives you an entire country or other large area. Large amounts of data will be slow in GIS software. If you know you can crop the data to a more manageable size, and you won't need the rest later, then go and get your bounding box now. Useful website for bbox stuff: http://bboxfinder.com/#0.000000,0.000000,0.000000,0.000000

## Process

1. Open up Terminal
2. Change directory to the folder with your PBF file
    ex. `cd ~/Desktop/osm_extracts`
3. If you don't need to crop the PBF file, then paste the following:
    `ogr2ogr -f "SQLite" -dsco SPATIALITE=YES name_of_new_file.db name_of_extracted_file.pbf`
    Suggestion: include the date in the filename so you know how old the data is. e.g. guinea-2mar2016
4. If you do need to crop the PBF file, then paste the following:
    `ogr2ogr -f "SQLite" -dsco SPATIALITE=YES -spat -16.68 3.97 -6.57 12.88 guinea-mar7.db guinea-mar7.pbf`
    The coordinates above are in the following order: West South East North
    `ogr2ogr -f "SQLite" -dsco SPATIALITE=YES -spat {x min} {y min} {xmax} {ymax} {output filename}.db {input file name}.osm.pbf`
5. That's it! You can load the spatialite file in QGIS or similar. 
6. Styles for the data can be found in teh qgis_styles repo: https://github.com/AmericanRedCross/qgis-styles

### Mapbooklet using QGIS and mailmerge
Parts of this may be more detailed than you need. The mailmerge part of this was done on a Mac. There will be some difference with a Windows setup. Please help improve this guide if you have additions or corrections.

Parts of this guide are still being documented/clarified.

This assumes you have loose leaf copier paper such as [Rite in the Rain LL851](http://www.riteintherain.com/inventoryD.asp?item_no=LL8511) with each sheet having two 4 5/8 in x 7 in pre-perforated loose leaf sheets (or something similar), QGIS, Microsoft Office, and geospatial data.

#### Spatiallite database, osm.pbf file, styling

original [source](http://anitagraser.com/2014/05/31/a-guide-to-googlemaps-like-maps-with-osm-in-qgis/) for some of the process

```
ogr2ogr -f "SQLite" -dsco SPATIALITE=YES -spat {x min} {y min} {xmax} {ymax} {output filename}.db {input file name}.osm.pbf
```
- *.qml style files are in [AmericanRedCross/qgis-styles](https://github.com/AmericanRedCross/qgis-styles) and also from [anitagraser](https://github.com/anitagraser/QGIS-resources/tree/master/qgis2/osm_spatialite)
- you may need coastline and a manually created "land" polygon (project background changed to blue, and land colored appropriately)



#### Creation of an atlas grid in QGIS:
- Create an AOI that can be used to build the grid
   - Draw it in a program that can save it as a geospatial data format
   - You could also use geojson.io
- Choose a scale for the atlas grid (we used 1:8,000)
- Project your AOI geometry into a meter-based projection (we projected the AOI from WGS84 to the local UTM projection)
- Determine the size of the quadrangle that will make up the grid
   - Take the scale and multiply it by the size of the paper on which it will be printed
   - For example, for __ by ___ inches size paper at 1:8,000 scale - using meters for the scale/paper conversion and for the projection we calculated ____ by ____ meters times 8,000 equals ______ by ____ meters for each quadrangle in the grid
   - 4 5/8" x 7" at 1:8,000 is a 939.8 x 1422.4 meter grid
- Use the Vector>Research Tools>Vector Grid tool in QGIS (or an equivalent tool) to build the specific grid size using the meters determined above (make sure the project space in QGIS is still in the meter-based projection)
- Re-project the grid back into WGS84 so that it matches up with most data sources - or project it into the projection appropriate for the area
- If you don’t want to use every part of the grid, remove the quadrangles that are not to be included in the atlas
- The final step is adding an attribute to the grid shapes that allows for the symbolization of the pages numbers - QGIS builds the grid from top-left to bottom-right, so once the consecutive numbers are added to the attribute table, it should read properly even if certain parts of the grid were removed
- In QGIS you can add a column using field calculater and use Record > $rownum for this

#### Atlas generation in QGIS:
- new print composer
- set custom page size
- set scale to 8000
- under map frame item properties check 'Controlled by atlas'
  - check fixed scale
- make sure grid is turned off
- atlas generation
  - check 'Generate an atlas'
  - choose grid as coverage layer
  - export as images

#### Mailmerge:
- Create a project folder and work in it
- Create an _images_ folder and drop all your map page images into it
- Create a white 1px by _1px blank.jpg_ file
- Get an ordered list of your files (on a Mac you can select all your files, copy, open TextEdit, go to Edit > Paste and Match Style) and put it into an Excel spreadsheet
- add page numbers in a new column
  - if filename is output_{number}.jpg
    - to remove file extension `=LEFT({cell},LEN({cell})-4)`
    - to remove first bit before the number `=RIGHT({cell},LEN({cell})-7)`
- add a column and auto-populate with row number
- add a column and use `=ISEVEN()`` on the row number
- sort... it should be a first group of odds (1,3,5..) and a second group of evens (2,4,6...)
- for each group separately repeat
  - redo row numbers (restart at 1 for the second group)
  - use `=ISEVEN()` and sort
- for the first group (odds) copy the bottom half up to the left of the first half but offset down by one and put 'blank.jpg' in the first one
- for the second group copy the bottom half up to the left of the first half and add a first row with index.jpg and cover.jpg
- your table should match the following:

first-left | first-right | first-leftnumber | first-rightnumber | second-left | second-right | second-leftnumber | second-rightnumber
-- | -- | -- | -- | -- | -- | -- | --
blank.jpg | output_1.jpg | 1 |  | index.jpg | cover.jpg |  |
output_3.jpg | output_5.jpg | 3 | 5 | output_4.jpg | output_2.jpg | 4 | 2
output_7.jpg | output_9.jpg | 7 | 9 | output_8.jpg | output_6.jpg | 8 | 6
output_11.jpg | output_13.jpg | 11 | 13 | output_12.jpg | output_10.jpg | 12 | 10
output_15.jpg | output_17.jpg | 15 | 17 | output_16.jpg | output_14.jpg | 16 | 14
output_19.jpg | output_21.jpg | 19 | 21 | output_20.jpg | output_18.jpg | 20 | 18

- Save as an .xlsx file
- Open a new Microsoft Word Doc and save as Word 97-2004 Document (.doc)
- Adjust the Top and Left page margins to match the punchouts of your paper, set Bottom and Right to 0
- Add a 3 column x 1 row table
   - Set the row height to match the height of the punchouts
   - Set the column widths to match the punchout, middle gutter, punchout
   - Adjust the Table Options to set the Default cell margins to 0
   - Remove cell border styling
- repeat on a second page
- Open the _Mail Merge Manager_ (in the Tools menu)
- Create new _Form Letters_
- _Get List_ > _Open Data Source..._ and select your Excel file
- In the left cell
   - _Insert Field..._ (in the Insert menu)
   - Choose the _INCLUDEPICTURE_ and add the directory path to your images folder for example `INCLUDEPICTUE "Macintosh HD:Users:danbjoseph:Desktop:BoundMapBook:images:"` then click okay
   - From _Insert Placeholders_ in the _Mail Merge Manager_ drag _leftside_ to the last part of directory path
   - The cell should now have something like `{ INCLUDEPICTURE "Macintosh HD:Users:danbjoseph:Desktop:BoundMapBook:images:output_1.jpg" \* MERGEFORMAT }`
- Repeat for the right-most cell but instead drag _rightside_ to the last part of the directory path
- in the lower left corner of each map-page on the first mailmerge page add a text box and fill with 'firstleft' and 'firstright' placeholders
- in the lower right corner of each map-page on the second mailmerge page add a text box and fill with 'secondleft' and 'secondright' placeholders
- _Complete Merge_ > _Merge to New Document_
- Select all then on a Mac press cmd+shift+option+u (Windows it should just be F9) to update all fields and the images should appear
   - You might need to toggle View all placeholders (the {a} icon) in the _Mail Merge Manager_ under _5. Preview Results_
   - If a path doesn't return an image, Word will drop in the last successful image (this is the reason for the blank.jpg for the empty cell for the cover page)
- Save as a PDF file
- Print double-sided and Actual size (not Fit or Shrink oversized pages)
- in the color copier (in the 3.5 pantry), use drawer 4 and put the paper so the holes towards the back side of the copier

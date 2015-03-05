### Mapbooklet using QGIS and mailmerge
Parts of this may be more detailed than you need. The mailmerge part of this was done on a Mac. There will be some difference with a Windows setup. Please help improve this guide if you have additions or corrections.

This assumes you have loose leaf copier paper such as [Rite in the Rain LL851](http://www.riteintherain.com/inventoryD.asp?item_no=LL8511) with each sheet having two 4 5/8 in x 7 in pre-perforated loose leaf sheets (or something similar), QGIS, Microsoft Office, and geospatial data.

#### Spatiallite database, osm.pbf file, styling

original [source](http://anitagraser.com/2014/05/31/a-guide-to-googlemaps-like-maps-with-osm-in-qgis/) for some of the process

```
ogr2ogr -f "SQLite" -dsco SPATIALITE=YES -spat {western long} {southern lat} {eastern long} {nothern lat} {output filename}.db {input file name}.osm.pbf
```
- *.qml style files are in [AmericanRedCross/qgis-styles](https://github.com/AmericanRedCross/qgis-styles)
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
- Use the Vector>Analysis>Vector Grid tool in QGIS (or an equivalent tool) to build the specific grid size using the meters determined above (make sure the project space in QGIS is still in the meter-based projection)
- Re-project the grid back into WGS84 so that it matches up with most data sources - or project it into the projection appropriate for the area
- If you don’t want to use every part of the grid, remove the quadrangles that are not to be included in the atlas
- The final step is adding an attribute to the grid shapes that allows for the symbolization of the pages numbers - QGIS builds the grid from top-left to bottom-right, so once the consecutive numbers are added to the attribute table, it should read properly even if certain parts of the grid were removed

#### Atlas generation in QGIS:
_to be added_

#### Mailmerge:
- Create a project folder and work in it
- Create an _images_ folder and drop all your map page images into it
- Create a white 1px by _1px blank.jpg_ file
- Get an ordered list of your files (on a Mac you can select all your files, copy, open TextEdit, go to Edit > Paste and Match Style) and put it into an Excel spreadsheet in column A
- Autofill column B with the row number (e.g. 1,2,3...)
- Autofill column C with the formula `=ISEVEN(<column B cell>)`
- Sort all the data on column C
- Fill column D with the the row number but individually for each of the column C TRUE/FALSE groups
- Autofill column E with the formula `=ISEVEN(<column D cell>)`
- Sort by Column C Then Column E
   - Your list should be main-grouped into Odd, Even and then sub-grouped into Odd-evens, Odd-odds, Even-evens, and Even-odds
   - Page 1,5,9...,3,7,11..., 2,6,10...,4,7,12..
- Delete all except Column A (your filenames)
- Cut/paste the sub-group of both main-groups up next to the first half, but for the group that has page number 2 offest down by one and put blank.jpg in the first cell, then remove the empty rows between the lists, add a column and fill it with the row number but individually for each of the two groups, add a column with the formula `=ISEVEN(<column C cell>)`
```
A              |  B              |  C  |  D  
-----------------------------------------------------
output_1.jpg   |  output_3.jpg   |  1  |  =ISEVEN(C1)  
output_5.jpg   |  output_7.jpg   |  2  |  =ISEVEN(C2) 
output_9.jpg   |  output_11.jpg  |  3  |  =ISEVEN(C3) 
output_13.jpg  |  output_15.jpg  |  4  |  =ISEVEN(C4) 
output_2.jpg   |  blank.jpg      |  1  |  =ISEVEN(C5)
output_6.jpg   |  output_4.jpg   |  2  |  =ISEVEN(C6)
output_10.jpg  |  output_8.jpg   |  3  |  =ISEVEN(C7)
```
- Sort by Column C Then by Column D, then delete those columns
- Add _leftside_ and _rightside_ column headers
- Your table should match the following format
```
leftside       |  rightside 
output_1.jpg   |  output_3.jpg
output_2.jpg   |  blank.jpg
output_5.jpg   |  output_7.jpg
output_6.jpg   |  output_4.jpg
output_9.jpg   |  output_11.jpg
output_10.jpg  |  output_8.jpg
output_13.jpg  |  output_15.jpg
```

__Note: if you want page numbers at the outside corner of each page your table should match the following format:__
- _the instructions above will be updated to reach this point shortly_
- _the following instructions need to be updated so that mailmerge does 2 pages at a time and includes the page number boxes_
```
first-left     |  first-right    |  first-leftnumber  |  first-rightnumber  |  second-left    |  second-right   |  second-leftnumber  |  second-rightnumber
blank.jpg      |  output_1.jpg   |  1                 |                     |  index.jpg      |  cover.jpg      |                     |
output_3.jpg   |  output_5.jpg   |  3                 |  5                  |  output_4.jpg   |  output_2.jpg   |  4                  |  2
output_7.jpg   |  output_9.jpg   |  7                 |  9                  |  output_8.jpg   |  output_6.jpg   |  8                  |  6
output_11.jpg  |  output_13.jpg  |  11                |  13                 |  output_12.jpg  |  output_10.jpg  |  12                 |  10
output_15.jpg  |  output_17.jpg  |  15                |  17                 |  output_16.jpg  |  output_14.jpg  |  16                 |  14
output_19.jpg  |  output_21.jpg  |  19                |  21                 |  output_20.jpg  |  output_18.jpg  |  20                 |  18
```


- Save as an .xlsx file
- Open a new Microsoft Word Doc and save as Word 97-2004 Document (.doc)
- Adjust the Top and Left page margins to match the punchouts of your paper, set Bottom and Right to 0
- Add a 3 column x 1 row table
   - Set the row height to match the height of the punchouts
   - Set the column widths to match the punchout, middle gutter, punchout
   - Adjust the Table Options to set the Default cell margins to 0
   - Remove cell border styling
- Open the _Mail Merge Manager_ (in the Tools menu)
- Create new _Form Letters_
- _Get List_ > _Open Data Source..._ and select your Excel file
- In the left cell
   - _Insert Field..._ (in the Insert menu)
   - Choose the _INCLUDEPICTURE_ and add the directory path to your images folder for example `INCLUDEPICTUE "Macintosh HD:Users:danbjoseph:Desktop:BoundMapBook:images:"` then click okay
   - From _Insert Placeholders_ in the _Mail Merge Manager_ drag _leftside_ to the last part of directory path
   - The cell should now have something like `{ INCLUDEPICTURE "Macintosh HD:Users:danbjoseph:Desktop:BoundMapBook:images:output_1.jpg" \* MERGEFORMAT }`
- Repeat for the right-most cell but instead drag _rightside_ to the last part of the directory path
- _Complete Merge_ > _Merge to New Document_
- Select all then on a Mac press cmd+shift+option+u (Windows it should just be F9) to update all fields and the images should appear
   - You might need to toggle View all placeholders (the {a} icon) in the _Mail Merge Manager_ under _5. Preview Results_
   - If a path doesn't return an image, Word will drop in the last successful image (this is the reason for the blank.jpg for the empty cell for the cover page)
- Save as a PDF file
- Print double-sided and Actual size (not Fit or Shrink oversized pages)

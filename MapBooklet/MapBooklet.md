### Mapbooklet using mailmerge
Parts of this may be more detailed than you need. I did this on a Mac. There will be some difference with a Windows setup. Please help improve this guide if you have additions or corrections.

This assumes you have:
- Loose leaf copier paper such as [Rite in the Rain LL851](http://www.riteintherain.com/inventoryD.asp?item_no=LL8511) with each sheet having two 4 5/8 in x 7 in pre-perforated loose leaf sheets (or something similar)
- An image file for each page of your booklet

Steps:
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

# QGIS: Tips and tricks for the print composer

We at the American Red Cross are committed to using (and improving) open source software whenever possible. We love QGIS, but the print composer can be pretty frustrating at first. After bashing our heads against the keyboard, we've come up with these tips and tricks to guide our new staff through the process.

First, set up your map in QGIS and make it look nice. We've got a couple of other workflows that document [getting OSM data into a spatialite database] (httpss://github.com/AmericanRedCross/workflows/blob/master/converting_pbf_into_spatialite.md) and our [QGIS style files] (httpss://github.com/AmericanRedCross/qgis-styles) are available here. We started with some of Anita Graser's styles and modified them for our typical map needs, adding in vector icons and other stuff. The vector files are included in the download but will probably need to be re-linked if you're using them.

## Getting started with the interface

Create a new print composer and give it a name. You'll see this interface appear:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/overview.png)

This is less intuitive than it seems, so a few intro notes:

1. (Red) The buttons on the top left are the different types of select tools that you're working with: point, zoom, select, and pan. Whichever one is selected will dictate how your pointing, clicking, and scroll wheel are impacting the map features. In general you'll want the select tool highlighted in order to work with the elements on the page (shapes, text, map, etc). If you want to be able to pan and zoom around within an element (like the map), then select the pan tool. If you want to zoom around on the page without actually resizing anything, then you want zoom. If weird things happen when you click your mouse, then you've probably got the wrong tool selected.

2. (Blue) There are buttons on the left for adding elements like the map, scale bar, etc.

3. (Orange) These menus on the right are critical for modifying any of the elements on your page. There's one for the composition itself, which you'll use to set up your canvas size, margins, number of pages, etc when you first open a new print composer window. There's another menu ("Item properties") for working with an element that you've selected. There are usually a ton of options and features buried in here.

4. (Yellow) Scroll bar. You're going to do a lot of work in the Item Properties menu, and it'll often involve scrolling down. Using the scroll wheel on your mouse will be frustrating - try to use this scroll bar instead.

5. (Pink) The print composer, like the map itself, works with layers. Use this menu for selecting the item you want to work with and for changing the order of items.

6. (Green) There's also an atlas creation tool - more on that on [this workflow page] (httpss://github.com/AmericanRedCross/workflows/blob/master/qgis-atlas-techniques.md).


## Getting the map on the page

1. Set up a new print composer and give it a name

2. Set up your document properties (page size, margins, etc)

3. Click the "Add map" button and draw in the map where you want it to appear.

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/general_setup.gif)

4. Sometimes what appears in your print composer doesn't exactly match what you see on your data view. The print composer will always peg what appears in your map to the bottom right-hand corner of what is in your data view. Once you know that, it's just a matter of re-sizing or scaling.

In case that doesn't make sense:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/preview2.png)
![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/preview.png)


## Moving and scaling

There are a few ways you can do this. The best way to move the content of the map is by clicking the "pan" tool and then clicking and dragging the map. You can also zoom in this way by using the scroll wheel, but it's easier to go over to the "Item properties" menu and just alter the scale number - you get more flexibility this way.

Tip: Click "View extent in map canvas" to make your data view mirror your print composer.

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/zooms.gif)

## Save your print composer and come back to it

At this point, save your print composer because of Murphy's Law.

We noticed that if you close out of QGIS entirely, then come back to the print composer, all you see is a blank page. This is really frustrating. Fear not, the map has not disappeared! Select the map and go over to "Item properties". Change the dropdown from "Rectangle" to "Cache", and everything will come back.

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/recover.gif)


##Scale bar

Add the scale bar. There are a lot of ways you can style this using the "Item properties" menu. One downside: unlike ArcGIS, QGIS doesn't allow you to save a scale style, so you have to do this every time. I would appreciate it if someone would develop this feature.

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/scale.gif)

##Legend

The same is true for the legend - you can do a lot of modifications to the default, but you can't save a default legend formatting and have to make these changes every single time. For that reason, I often find it faster to make a legend in Adobe Illustrator (or Gimp or Inkscape if you want a free version) and stick it on top of my finished map, but it can be done in QGIS:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/legend.gif)

There are a couple of useful features in here, like being able to turn off the auto-updating layers, and being able to lock certain aspects.

There are a couple of blocks with doing a legen in QGIS. If you've got complicated symbology (like a vector symbol inside of a polygon), then the sizing will be weird - the vector will probably be way too big for the polygon in the legend. You can't just make everything in the legend bigger, convert to graphics (because this isn't a feature in QGIS), and resize. You could get around this by going back into the map and resizing your vector fills (and then save the style so you don't have to do it again) but even then, I had issues where some vectors were offset just a little bit in the legend, for no apparent reason (I double checked everything):

##Titles and drawing elements

For finishing touches, QGIS can actually do a lot more than you'd expect.

There's a basic shapes-drawing feature (no custom polygons, unfortunately) that allows you to add effects like drop shadow, inner glow, etc:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/title.gif)

You can add images (including vectors) for logos:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/image.gif)

And there's the text feature:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/text.gif)

##Output

Save the print composer and export your map as a PNG or a PDF. Don't export it an SVG; you won't be happy.

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/save.gif)

##The End

From all of these tools, we've been able to make some pretty nice-looking maps with just QGIS:

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/roads_example.png)

![] (https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/ut_example.png)

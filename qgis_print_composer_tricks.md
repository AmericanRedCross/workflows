# QGIS: Tips and tricks for the print composer

We at the American Red Cross are committed to using (and improving) open source software whenever possible. We love QGIS, but the print composer can be pretty frustrating at first. After bashing our heads against the keyboard, we've come up with these tips and tricks to guide our new staff through the process.

First, ~~set up your map in QGIS and make it look nice.~~ UPDATE: Begin with the end in mind. Thanks to Nyall Dawson for reaching out with some tips and showing us a better way! Our new workflow is to drop in the basic layers and set up the print composer, then go back and do the styling later.

## Getting started with the interface

Once you've got your basic layers added, create a new print composer and give it a name. You'll see this interface appear:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/overview.png)

This is less intuitive than it seems, so a few intro notes:

1. (Red) The buttons on the top left are the different types of select tools that you're working with: point, zoom, select, and pan. Whichever one is selected will dictate how your pointing, clicking, and scroll wheel are impacting the map features. In general you'll want the select tool highlighted in order to work with the elements on the page (shapes, text, map, etc). If you want to be able to pan and zoom around within an element (like the map), then select the pan tool. If you want to zoom around on the page without actually resizing anything, then you want zoom. If weird things happen when you click your mouse, then you've probably got the wrong tool selected.

2. (Blue) There are buttons on the left for adding elements like the map, scale bar, etc.

3. (Orange) These menus on the right are critical for modifying any of the elements on your page. There's one for the composition itself, which you'll use to set up your canvas size, margins, number of pages, etc when you first open a new print composer window. There's another menu ("Item properties") for working with an element that you've selected. There are usually a ton of options and features buried in here.

4. (Yellow) Scroll bar. You're going to do a lot of work in the Item Properties menu, and it'll often involve scrolling down. Using the scroll wheel on your mouse will be frustrating - try to use this scroll bar instead.

5. (Pink) The print composer, like the map itself, works with layers. Use this menu for selecting the item you want to work with and for changing the order of items.

6. (Green) There's also an atlas creation tool - more on that on [this workflow page](https://github.com/AmericanRedCross/workflows/blob/master/qgis-atlas-techniques.md).


## Getting the map on the page

1. Set up a new print composer and give it a name

2. Set up your document properties (page size, margins, etc)

3. Click the "Add map" button and draw in the map where you want it to appear.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/general_setup.gif)

4. Sometimes what appears in your print composer doesn't exactly match what you see on your data view. The print composer will always peg what appears in your map to the bottom right-hand corner of what is in your data view. Once you know that, it's just a matter of re-sizing or scaling.

In case that doesn't make sense:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/preview2.png)
![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/preview.png)


## Moving, scaling, and locking it down

There are a few ways you can scale and pan the map in the print composer. The best way to move the content of the map is by clicking the "pan" tool and then clicking and dragging the map. You can also zoom in this way by using the scroll wheel, but it's easier to go over to the "Item properties" menu and just alter the scale number - you get more flexibility this way.

Tip: Click "View extent in map canvas" to make your data view mirror your print composer.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/zooms.gif)

Next, take the scale on your print composer and apply it to the map canvas, then lock it down. This allows you to style the map layers, knowing that they'll look the same in the print version as they do in your canvas. If you need to zoom in and out to check details, use the magnifier tool.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/lock_scale.gif)

## Save your print composer and come back to it

At this point, save your print composer because of Murphy's Law.

We noticed that if you close out of QGIS entirely, then come back to the print composer, all you see is a blank page. This is really frustrating. Fear not, the map has not disappeared! Select the map and go over to "Item properties". Change the dropdown from "Rectangle" to "Cache", and everything will come back.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/recover.gif)

## Style your layers

Once the print composer is set up, you can style your layers in the map canvas.

A few basic tips (thanks again to Nyall for showing me these):

Using the style dock will save a lot of clicking and waiting. Click the paintbrush button above the layers panel and the dock will appear on the right. You can switch between layers and the changes will update in real time.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/style_dock.gif)

Also, data labels really can be manually moved. To do this, put a layer into edit mode and add an X and Y column (set the columns to decimal numbers). Save the changes but keep the editor on. In the style dock, go to the labels settings and scroll down to data-defined properties. Link the coordinates to the X and Y columns. Now you can use the "move label" tool to click and drag a label. This will automatically update the X and Y columns in the attribute table with the offset. Remember to save the edits when you're done.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/move_label2.gif)

Data-defined properties can be used to dictate all kinds of other styling - there are some great explanations and examples online.

Also, you can set layer presets which saves the layers that you want to include in the print composer - that way you can turn layers on and off without worrying that it'll affect the print view. This also makes it a lot easier to work with multiple maps on a print composer.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/preset_layers.gif)

For working with OpenStreetMap data in specific, we have a couple of other workflows that document [getting OSM data into a spatialite database](https://github.com/AmericanRedCross/workflows/blob/master/converting_pbf_into_spatialite.md) and our [QGIS style files](https://github.com/AmericanRedCross/qgis-styles) are available here. We started with some of [Anita Graser's styles and tips](https://anitagraser.com/2014/05/31/a-guide-to-googlemaps-like-maps-with-osm-in-qgis/) and modified them for our typical map needs, adding in vector icons and other stuff. The vector files are included in the download but will probably need to be re-linked if you're using them.

Once you've styled the layers, go back and finish your map.

## Scale bar

Add the scale bar. There are a lot of ways you can style this using the "Item properties" menu. ~~One downside: unlike ArcGIS, QGIS doesn't allow you to save a scale style, so you have to do this every time. I would appreciate it if someone would develop this feature.~~ Update: This is now available in v2.16. Thanks to whoever made that possible :) You can save the entire print composer as a template, or you can make a print composer with just the scale bar and save that, then add it into a future map.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/scale2.gif)

## Legend

I'm really excited that I can now save legend templates. Legends are pretty straightforward in QGIS:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/legend.gif)

There are a couple of useful features in here, like being able to turn off the auto-updating layers, and being able to lock certain aspects.

There are a couple of blocks with doing a legend in QGIS. If you've got complicated symbology (like a vector symbol inside of a polygon), then the sizing will be weird - the vector will probably be way too big for the polygon in the legend. You can't just make everything in the legend bigger, convert to graphics (because this isn't a feature in QGIS), and resize. You could get around this by going back into the map and resizing your vector fills (and then save the style so you don't have to do it again) but even then, I had issues where some vectors were offset just a little bit in the legend, for no apparent reason (I double-checked everything).

## Titles and drawing elements

For finishing touches, QGIS can actually do a lot more than you'd expect.

There's a basic shapes-drawing feature ~~(no custom polygons, unfortunately)~~ (Update: custom polygons are here! Time to update my version of Q) that allows you to add effects like drop shadow, inner glow, etc:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/title.gif)

You can add images (including vectors) for logos:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/image.gif)

And there's the text feature:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/text.gif)

##Output

Save the print composer and export your map as a PNG or a PDF. Don't export it an SVG; you won't be happy.

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/save.gif)

##The End

From all of these tools, we've been able to make some pretty nice-looking maps with just QGIS:

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/roads_example.png)

![](https://arcmaps.s3.amazonaws.com/Training%20Materials/QGIS_workflow_images_gifs/ut_example.png)

# West Africa OMK Data-Cleaning Tutorial

## Before we start

So you've mapped over 5,000 communities in West Africa, that's pretty cool! But now, we have all of this data to clean, so that it can be used by people and organizations working in your communities. 

Please familiarize yourself with the [osmwiki](http://wiki.openstreetmap.org/wiki/Map_Features) as it will be a crucial tool for cleaning data. We want most if not all of our tags to be within the wiki so that they are recognized by the community and useful for any people or organizations who may use the data in the future.

Your months of work in the border areas of Liberia, Guinea, and Sierra Leone have provided critical map data, which would otherwise not be available had it not been for the tireless efforts of the volunteers who visited all of these communities. This data will be crucial in the event of a disaster or epidemic.


### Things to Download
[JOSM](https://josm.openstreetmap.de/download/josm.jnlp)

[OpenRefine](http://openrefine.org/) - To Use in browser: 127.0.0.1:3333

### Resources We Will Use
ToDo List Plugin

OpenData Plugin

[osmwiki](http://wiki.openstreetmap.org/wiki/Map_Features)

[geojson.io](http://geojson.io)

## Table of Contents
1. [List of Data to Clean](##list-of-data)

2. [Pre Cleaning](##pre-cleaning)

3. [Initial Purging](##initial-purging)

4. [Cleaning New Points](##cleaning-new-points)

5. [Cleaning Existing Polygons](##cleaning-existing-polygons)

6. [Cleaning Placeholders](##cleaning-placeholders)

7. [Source](##important)

8. [Uploading](##uploading)

9. [Afterward](##afterward)

## List of Data

### Liberia (NHQ to clean and upload)

* ~~Liberia_Community_survey_v18 (1st Round)~~
* Liberia_Community_survey_v18 (2nd Round)
* Buildings
* Building Placeholders
* Buildings with POIs
* Points of Interest Africa
* Africa Health Facilities (Both Liberia and SL)
* Schools
* Water Points Africa

### Sierra Leone (Mapping Hub to clean and upload)

* Africa Health Facilities (Purge Liberia data)
* SL Building Placeholders
* SL Buildings
* SL Buildings with POIs
* SL Points of Interest
* SL Schools
* SL Water Points

### Guinea (Mapping Hub to clean and upload)

* French buildings v1
* French Building Placeholders v1
* French Buildings wtih POIs v1
* French POIs v1
* Guinee_OMK_V1-1-2
* French Schools v1
* French Water Points Africa v2

##Pre-Cleaning

Create folder structure to organize data
raw
working
final

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/folder-structure.png)

Download Data from [omkserver.com](omkserver.com)


Install ToDo List Plugin, OpenData Plugin


##Initial Purging

Open JOSM
Install To-Do List Plugin

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/purge.gif)

Begin to PURGE all non-relevant features CTRL+SHIFT+P (landuse, railroads) DO NOT DELETE

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/search_all.png)

If you want to only focus on a small geographical region of the data, purge everything outside of that region and SAVE

Right-click, save to your working folder and name it relevant to the dataset, adding a "_1" to the end of the file name. Each iteration of your file will be a new version of your data, so you know that you are working with the most current version. 


###Points vs Polygons?

_Some layers have both points and polygons, we want to separate the points and the polygons as they have to be uploaded separately._ 

After you've purged all of your unwanted data, save your OSM file. We are going to create separate files for both the points and the polygons. 

Select `File>New Layer` to add a new layer that we will be using for the polgons

Press CTRL+F to bring up the search box. Type `type=way`, and Start Search. This will select all the polygons. Press `CTRL+C` to copy the building polygons, then select your new layer, you'll know it is selected because the green check mark will move to that layer, and the data in your original layer will be greyed out. We will now paste the data here by pressing `ALT+CTRL+V`, this will ensure that the data gets pasted in its original position. 

##Cleaning New Points

Open your browser and go to geojson.io, select "Open" and open your "feature_1.osm" file in the window. Then select `Save>CSV`

Use OpenRefine

Open OpenRefine, no user interface will pop up

In your browser navigate to `127.0.0.1:3333`

click `Create Project`

select `Choose Files` and navigate to your points_2.csv file in your working folder

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/openRefine-create.png)

"Parse data as CSV/TSV/separator-based files" and select `Commas` under `columns are separated by`

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/openRefine-csv.png)

Give the project a name related to your data set and select `Create Project`

Across the top you will see our different fields. We will need to standardize each of these using "Facets"

Select the drop-down next to your first column and navigate to "Facet>Text facet." This will bring up a list of each uniuqe value in our field. Note that many are similar but are not grouped together due to misspellings, the addition of "town" or "community" to a name, capitalization of words, extra spaces between words, etc. These are the issues we want to address.

Above this box, select "Cluster." This will bring up a new window where we can begin to cluster like values.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/openRefine.gif)

Be sure to check through each methodology for clustering, as different techniques may find different clusters.

We need to do this for each column in the data.

**Be sure to check the data in the facet to see if there are any issues you can address on individual entries.**

When we are done cleaning in OpenRefine. We need to export the file as a .csv file.

Click `Export>Comma Separated Value`

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/openRefine-export.png)

This will download the file as a .csv, be sure to save it in your working directory using your naming convention that you've already established.

We can now open the .csv in JOSM by selecting `File>Open`

Click `OK` to the WGS84 GCS. This refers to the coordinate system that the data is in. 

Now we will see all of the points on the map in the correct location.

Press `CTRL+A` to select all of the points. Then on the to-do list window, press the `Add` button.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/todo-list.png)

We will now examine each individiual point to ensure that it is in the correct location. Use bing imagery or OSM basemaps if possible.

[Ready To Upload](##important)

##Cleaning Existing Polygons

_In this section we will cover the cleaning of building data where the buildings already exist in OpenStreetMap, and we want to preserve their version histories._

This will be a bit more tedious, as all of the cleaning must be done in JOS.

To begin we will select all the polygons in the layer by pressing `CTRL+A`.

In the Tags/Memberships window, we will see each different key and value pair in the dataset.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/key-values.png)

We want to go through each value to make sure we have no spelling errors, or mis-entered data.

[Ready To Upload](##important)

##Cleaning Placeholders

Follow the OpenRefine steps for [Cleaning New Points](##cleaning-new-points).

Bring .csv back into JOSM

Select `File>New Layer`

You can toggle between layers here, make sure your new layer is the one that you are downloading and adding data to.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/layers.png)

Trace new buildings in your new data layer

Copy and Paste key/value pairs from the cleaned .csv layer to your new data layer.

[Ready To Upload](##important)

##IMPORTANT

Add `source="Red Cross Field Survey"`

Go through each individual entry in the data using the "ToDo List" plugin to ensure that each point being added has a main tag. `building=`, `amenity=`, `man_made=`

##Uploading

Once everything has been standardized and you've gone through ever point in the to-do list, you can upload. Click the upload icon.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/upload.png)

Address any validation errors that occur, we want our upload to be clear and error-free.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/validate.png)

Changeset comments should be: `"Uploaded ______(feature, schools, buildings, POIs, etc) data from Red Cross field survey #MissingMaps #WestAfricaHub #RedCross"`

Data source, type in "Red Cross survey"

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/west-africa-data/finalUpload.png)

When uploading there may be some data conflicts with current data. Address these on a case by case basis. Most of this should be addressed by purging the unecessary data in the beginning.

##Afterward

Save your uploaded OSM file in your directory as a .osm file. All of which will be sent to NHQ.

If anyone from the OSM community comments on one of your changesets, or sends you a message regarding the upload of your data. Respond to them in a timely and polite manner. Answer any questions they may have, OpenStreetMap is a community effort collaboration is important! 



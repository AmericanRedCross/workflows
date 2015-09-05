## OpenMapKit (OMK)
https://github.com/americanredcross/openmapkit/wiki

### What OMK does well, what it doesn't do
- buildings and roads
- currently no creation of new features
  - features need to be pre-traced
- currently doesn't handle points
  - one of the next features to be added will be the ability to create new points
- dense areas are tough
  - decreased GPS accuracy
  - requires greater map literacy


### Creating the survey
- XLSForm syntax: basic
  - http://xlsform.org/
- XLSForm syntax: adding the OpenMapKit question type
  - https://github.com/AmericanRedCross/OpenMapKit/wiki/OpenDataKit-Forms-for-OpenMapKit
- form design: OSM tags, caveats, tips & tricks
  - if a key is part of the survey and a feature has a pre-exisiting value that is not included in the options list, then that value will not display in the question interface
  - use [taginfo](https://taginfo.openstreetmap.org) to research if keys/values are commonly used
  - don't include the same tags on two objects. [One feature, one osm element](http://wiki.openstreetmap.org/wiki/One_feature,_one_OSM_element)
  - when providing name=* for a highway or addr:street=* for a building
    - don't abbreviate (for example, use "Road" and "Lane" NOT "Rd" and "Ln")
    - use title case, capitalize the first letter of each word

### Setting up the app
- install ODK Collect and OpenMapKit on a phone
  - the next version of ODK when published to the Google Play Store should include all necessary functionality but for now you will need to use the APK files downloadable from the [wiki](https://github.com/AmericanRedCross/OpenMapKit/wiki/Downloads)
    - download directly to you phone or copy both files over from your computer
    - use the phone's file browser to open the files to install
    - you may need to install a file browser such as ES File Explorer File Manager
    - you may need to change the security settings on the phone to allow installation of apps from unknown sources
    - do not update ODK Collect

### Setting up the cloud-based data repository
- set up an account on [ONA](https://ona.io/)
  - there is a free account level
  - soon will have the code and instructions up on formhub to run your own server instance
- upload your survey(s)
- configure your app
  - open the ODK Collect app, go to 'General Settings' then 'Configure platform settings' and change the URL
- download the surveys to the phone
  - from the main ODK Collect menu go to 'Get Blank Form'
  - you can also manually place the survey file(s) on the phone, from ONA go the survey page and download the XForm version and place it in the `odk/forms` folder on the phone

### Generating mbtiles for offline basemap in OMK
- install [node](https://nodejs.org/)
  - install the following packages tl, mbtiles, tilelive-http
  - `npm install -g tl mbtiles tilelive-http`
- go to http://bboxfinder.com/ and box your area
  - it should return your coordinates in the following order: lng-min, lat-min, lng-max, lat-max
- open terminal/command line and `cd` to your project folder and run the following:
  - `tl copy -z 13 -Z 20 -b '{{lng-min}} {{lat-min}} {{lng-max}} {{lat-max}}' 'http://a.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png' mbtiles://./{{myFileName}}.mbtiles`
  - it should begin saving the map tile images one by one and compiling them in the folder
  - *NOTE:* larger areas can take a number of hours

### Downloading OSM data
- change the coordinates order to lat-min, lng-min, lat-max, lng-max (2, 1, 4, 3) and add back the commas
- go to http://overpass-turbo.eu/ and enter the following:
  - `way[building]({{lat-min}}, {{lng-min}}, {{lat-max}}, {{lng-max}});out meta;>;out meta qt;`
  - replace 'building' with 'highway' if surveying roads
    - *NOTE:* roads will need to be split and combined into a logical network (for example you don't want a single line segment that carries through corners)
  - click 'Run' and 'continue anyway' if a warning pops up
  - click 'Export' and choose 'raw data directly from Overpass API' and add a \*.osm file extension when saving
- copy both files to your phone
  - in the root directory there should be `openmapkit/mbtiles` and `openmapkit/osm`
  - copy the files into the respective folders

### Separation of ODK and OMK data
- some data doesn't belong in OSM, but you can still collect it with this workflow, just include them as questions on the 'survey' tab of your form workbook and not in the lists on the 'osm' tab

### Field survey methods (e.g. integration of Field Papers and OMK)
- OMK is a useful option when collecting many details about each feature such as building type, name, number, material, and condition
- [Field papers](http://fieldpapers.org/) are used to collect other data including major landmarks, water sources, sanitation points and corrections to the traced base map
- Field papers are also useful for collecting specific data each community deems priority such as landslides, flood prone areas, informal dumpsites (can include sensitive data that does not need to go into OSM)
- the map on the phone used for the OMK matches the map on the field paper, which helps users with orientation and collecting accurate data


### Retrieving the collected data
- the survey data can be downloaded as a spreadsheet (\*.csv or \*.xls)
  - it will not include any tag data entered via OpenMapKit
  - it will contain a column with the OSM way IDs, and you can use this to spatially join the survey data to features downloaded from OSM and loaded into a GIS software
- the OpenMapKit data can be downloaded as an \*.osm file
  - quality control and validation should be carried out in JOSM before uploading the changes to OSM
  - if the data contains features with changed tags that you do *not* want to upload to OSM, you will need to turn on 'Expert mode' in the preferences of JOSM and then use the 'Purge...' command from the main menu Edit dropdown (this will leave the buildings on the server as is, if you delete them from your OpenMapKit \*.osm file it will delete them from the server, read more about [purge](https://josm.openstreetmap.de/wiki/Help/Action/Purge) on the JOSM wiki)

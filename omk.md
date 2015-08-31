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
- form design: OSM tags, caveats, tips & tricks, current limitations

### Setting up the app
- install ODK Collect and OpenMapKit on a phone
  - the next version of ODK when published to the Google Play Store should include all necessary functionality but for now you will need to use the APK files downloadable from the [wiki](https://github.com/AmericanRedCross/OpenMapKit/wiki/Downloads)
    - download directly to you phone or copy both files over from your computer
    - use the phone's file browser to open the files to install
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


### Field survey methods (e.g. integration of Field Papers and OMK)

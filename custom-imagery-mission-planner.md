## Load custom imagery into Mission Planner

This method for getting custom imagery into mission planner is... involved. But it works! Custom imagery here references imagery from some imagery service and the motivation for taking it offline into mission planner is so you can use imagery in mission planner when internet connections are not around.

Also note - mission planner here is PC only. There is a mac equivalent to mission planner (APM Planner), though this method for adding imagery described below will only work for the pc install.

The basic steps are to:

1. Pick an image extent and imagery service, and download said extent at a *single* zoom level and save it as mbtiles. This is done using [tl](https://github.com/mojodna/tl), a node.js package.
2. Unpack the mbtiles file into a geotiff with GDAL
3. Load that geotiff as a layer into geoserver
4. Use the generated geoserver WMS link in mission planner.

### map extent to mbtiles

1. First you'll need to select a mapping extent. For this tutorial we'll use the extent of Culasi, Philippines. 
	- Using [bboxfinder.com/](http://bboxfinder.com/) draw a bounding box around the city and grab the bounding box coordinates at the bottom of the page next to where it says 'box' 
	
		![bboxfinder-culasi](https://arcmaps.s3.amazonaws.com/share/blog-pictures/bboxfinder-culasi.png)

	- here they'll be roughly 122.032185,11.396067,122.081280,11.440320. keep those handy somewhere.
		
2. Next, you'll need to globally install (the `-g` flag) [tl](https://github.com/mojodna/tl) and some dependencies. The version of node can be finicky but we've gotten it to work with `v0.10.36`. 
	```
	npm install -g tl mbtiles tilelive-http
	```
3. After installation completes you should be able to use the following command.

	```
	tl copy -z 18 -Z 18 -b '{{lng-min}} {{lat-min}} {{lng-max}} {{lat-max}}' 'http://some.imagery.service/{z}/{x}/{y}.png' mbtiles://./{{myFileName}}.mbtiles
	
	``` 


### mbtiles to geotiff

At this point you should have imagery in  .mbtiles format.

1. There is just one step to convert to geotiff. So long as you have [gdal](http://www.gdal.org/) downloaded as a cli, run the following command in terminal to convert your motiles to a geotiff. Note that the culasi.tiff file is not too large, but as you start trying to download larger and larger extents, image size will grow!

	```
	gdal_translate -of GTiff culasi.mbtiles culasi.tiff

	``` 
	
Now we are ready for geoserver!

### geotiff to geoserver

1. First we'll need to [download geoserver](http://geoserver.org/download/). For this tutorial the stable (2.11) release was used
2. Once downloaded, open geoserver by searching for it on the windows' start menu, then go to the local server path shown in the cmd window that pops up when geoserver is started
3. Once you have geoserver opened, use the username and password generated when you installed (default as usr:admin, pas:geoserver). This should lead you to the following screen.
	
	![geoserver-home](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-home.png)
	
	You'll notice the ability to add workspaces, stores, and layers. Per my very short time getting to know geoserver, I think of a workspace as a sort of file directory for data, stores as the actual geodata we want to render and serve as tiles, and layers as those actual tiles. 
	
4. To alleviate any confusion click each of workspaces, stores, and layers individually, and delete the default stores,layers,and workspaces. So, in the case of layers, click it on that welcome page and on the next page select the checkboxes next to each of the layers then click ```Remove Selected```

	![geoserver-removeLayers](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-removeLayers.png)
	
5. With a clean geoserver slate, create a new workspace. **repeat this and the following steps for each geotiff you want to use in mission planner**
	1. Click ```create workspace``` on the welcome page
	2. On the next page give your new workspace a name, namespace uri, and set it as the default workspace. For this tutorial's purposes, name it 'culasi' and give the name space uri as culasi.org (this just needs to mimic a link...so I do believe). Then be sure to set it as the default workspace and select ```WMS``` under ```services```
	3. It's ok if you click ahead before setting this workspace as the default. If you click on workspaces in the data menu on the left hand side, you'll be able to set it as such.

		![geoserver-wms](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-wms.png)

	5. Once all these are parameters are set, save it. If you want to double check you've made it the default, click workspaces on the lefthand side again. You should see a checkmark next to the workspace. 
	
6. Next we need to add our culasi geotiff as a data store. Do this by selecting ```add store``` on the welcome page.
	
	1. On the next page, select ```GeoTiff``` found among the other options under ```Raster Data Sources```
		![geoserver-datasource](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-datasource.png)
	
	2. On the following ```Add Raster Data Source``` Page, make sure the 'culasi' workspace is selected. Then give the imagery a name. Like all things in this tutorial, we'll use culasi. Also, add a description if you'd like. Then, select ```browse``` next to the dropdown under ```connection parameters``` and navigate to the culasi.geotiff file we made. After doing all that, the page should look like this.

	
		![geoserver-addraster](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-addraster.png)
	
	3. Save it, and on the next screen click publish.
	4. On the NEXT screen, under Coordinate Reference systems, set the the declared SRS to plain WGS by searching for the code ```4326```. **YOU NEED TO SET THE DECLARED SRS TO THIS OR IT WILL NOT WORK**
	
		![geoserver-crs](https://arcmaps.s3.amazonaws.com/share/blog-pictures/geoserver-crs.png)
		
	5. Last, scroll to the bottom and click save.
	
**Now we are ready for mission planner!**

## geoserver wms link in ‘customWMS’ imagery source for mission planner

1. If you do not already have mission planner, [download it](http://ardupilot.org/planner/docs/common-install-mission-planner.html)
2. With it downloaded, open it and navigate to flight plan, using the flight plan button at the top of the screen.
3. On the flight plan screen, click the drop down under the ```grid``` and ```view kml``` buttons, and choose WMS Custom.
 
	![missionplanner-customwms](https://arcmaps.s3.amazonaws.com/share/blog-pictures/missionplanner-customwms.PNG)
	
4. A new popup will appear asking for a link to imagery. Use the link localhost:PORT/name-of-workspace-you-saved-geotiff/wms. For the culasi example, this turns out to be localhost:5000/culasi/wms

	![missionplanner-wmsurl](https://arcmaps.s3.amazonaws.com/share/blog-pictures/missionplanner-wmsurl.PNG)

5. Next it will ask which layer you want and to type the corresponding number. Since we just have one layer, type zero.
	![missionplanner-wmslayer](https://arcmaps.s3.amazonaws.com/share/blog-pictures/missionplanner-wmslayer.PNG)

6. Once you've done that click ```flight data``` and with a little patience, you have custom imagery!

	![missionplanner-customImagery](https://arcmaps.s3.amazonaws.com/share/blog-pictures/missionplanner-customImagery.PNG)
	![missionplanner-culasi](https://arcmaps.s3.amazonaws.com/share/blog-pictures/missionplanner-culasi.jpg)

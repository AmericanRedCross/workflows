#Fixing West Africa Community Names
![Missing Maps](http://wiki.openstreetmap.org/w/images/thumb/a/a3/Missing-Maps-logo.jpg/400px-Missing-Maps-logo.jpg)
# 
## West Africa Project Overview

During the Ebola Reponse, spatial data was either non-existant or out of date for many communities in the border regions of Guinea, Liberia, and Sierra Leone. This motivated Missing Maps to collect data throughout a 15km buffer of these countries' borders by conducting community surveys. 

The data Missing Maps generated will be released in the coming months on OpenStreetMap and will be useful for activities like determining vulnerability to public health issues in these parts of West Africa. 

### Your Contribution to the Project

Tonight you all will ensure places visited during Missing Maps' surveys are correctly named and tagged in OSM.

# 
![JOSM Icon](https://josm.openstreetmap.de/browser/trunk/images/logo.png?format=raw)
# 

### What is JOSM?
The Java OpenStreetMap Editor (JOSM) is a desktop program for editing and uploading data to OSM. With a suite of plugins that help do things like manage mapping tasks and draw buildings more quikly, it very useful to know for those interested in frequently contributing to OSM.

### JOSM Setup


1. Download [JOSM](https://josm.openstreetmap.de/download/josm.jnlp)

2. [Install](http://wiki.openstreetmap.org/wiki/JOSM/Plugins#Installation) needed plugins: 

	* Go to the JOSM dialogue in the top tool bar and select preferences. 
	
	* In the window that appears select plugins along the left hand side
	
		![Plugins Icon](http://wiki.openstreetmap.org/w/images/2/2f/IconeGreffons.png)

	* Search for each of the following plugins by typing them in the search bar. Once you've found them, click the box to the left of their description so that a check mark appears.

		* OpenData
	
		* utilplugin2
	
		* todo
	
		* building tool	
	
	* Once all are selected click the "download list" button, then click ok.
# 

3. Set up the three data layers needed for tonight

	* OSM Data Layer
	
		* Navigate to the "File" dialogue in the tool bar and select "New Layer"
		
			![New File Icon](https://josm.openstreetmap.de/export/11346/josm/trunk/images/new.png)
			
		* A layer named "Data Layer 1" will appear in your layers list found on the right hand side of the screen. Right click it and select "Rename Layer" and give it a distinct name. i.e "westafrica_communities".		
			  
	* Field Survey Layer
		* Once the 100 Communities shapefile has been trasferred from the flashdrive to your computer, again go to the "File" dialogue and select "Open".  
				
			![Open File Icon](http://wiki.openstreetmap.org/w/images/3/3c/JOSM-Icon_Datei_%C3%B6ffnen.jpg)
			
		* Then navigate to the file and select it This too will be in your "Layer List".
	
	* OSM Basemap
		* Navigate to the "Imagery" dialogue in the top tool bar. From the dropdowm select "OpenStreetMap Carto (Standard Layer)". This too will show up in your "Layer List" and will make a OSM basemap appear in the map pane within JOSM. 
		
				
	
### Fixing Community Names Workflow

1. Add your 100 communities within your 100 communities layer to your todo list. 

	* Click the todo list icon found on the lefthand side of JOSM
	
		![todo icon](http://i.imgur.com/0UymMtH.png)

	* This will make a todo list appear on the left hand side of you screen		
	* With your 100 communities layer toggled, first click the "S" key on your keyboard, then once on the map with your mouse, then finally **command+A**, this will select all buildings in the layer. Then click the "Add" button on the todo list. You should have your list looking something like [this](http://imgur.com/a/5Zq7w).
# 
2. Go one by one through each of the points in your todo list. Check to see if the OSM Basemap has a name for the community you are flown to.

	* If there is not a community name in the OSM Basemap, toggle to your OSM Data Layer within the "Layer List" and add a point by clicking "A" on your key board, then double clicking on the map. Then, **with your OSM Data Layer still selected **, click the "add" button within the "Tags/Membership" list. A new window will pop asking to please add a value and a key. Do this three times to add the following three key/value pairs: 
	
		* A `place` key with one of the following values:
			
			* `town`
			
			* `village`
			
			* `quarter`
			
			* `hamlet`
			
			* `farm`
# 	
		* An `addr:city` key with the value equal to the value held in the 100 builings shapefile's `namvill` tag. 
		
			* note, before adding this key/value pair you will have to go to your buildings layer and find the `namvill` tag's value
# 
		* A `source` key with the value `Red Cross Field Survey`		
# 
	*  If there is a place name already within the OSM Basemap check to see if it matches the `namvill` tag of the Field Survey layer. If it does not, toggle to your OSM Data Layer in the "Layer List" and click the "download map data from osm server" button (the third one over from the top left)
	
		![Download buttom](https://josm.openstreetmap.de/browser/trunk/images/download.png?format=raw)

	* This will download the osm data underlying the OSM Basemap to your OSM Data Layer and allow you to edit it. 
		* Find the point within the downloaded data holding the town name and change it accordingly. Make sure to also give that point the same key value pairs mentioned above. 
# 
			* There many not be an `addr:city` tag, so delete whatever else was there holding the community name and add the right `addr:city` tag.  
# 
	* **If the existing point within the osm data you downloaded has a** `fixme` **tag, remove it if we've addressed the name**
# 
3. After every 5 places you have correctly tagged, save the OSM Data Layer and commit a changeset to OSM. 

	* Click the "upload all active changes to active data layer to osm server button" 
	
		![Upload Icon](https://josm.openstreetmap.de/browser/trunk/images/upload.png?format=raw)
	
	* Within the window there will be a comments form. Add the following comment: 
	
		* *Updated community names based on Red Cross field survey of 7,000 communities in West Africa #redcross #missingmaps #westafricahub #wacf*
		
*#wacf stands for "West Africa Community Fix"*

### Helpful Information

##### *Toggling Between Data Layers*

To toggle between data layer click just left of the data layer you want to toggle to within the layers list. Upon your click a green check mark should appear and the data within that layer will show up in the map pane.

##### *Showing Tags and Memberships*

To show tags and memberships for a data layer first click the "S" key on your keyboard. This allows you to select features in the map pane. Then click the feature in the map pane you want to see the tags.

##### *Todo list quirks*
To be 'flown' between features in your to do list, make sure the "Field Survey Layer" is selected in the "Layer List" first. Then simply click on them within the list and you will be sent to them! Also, to mark features as 'done' on the to do list make sure to select that feature in the list then click the 'mark' button. 


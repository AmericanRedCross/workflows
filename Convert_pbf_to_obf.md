Creating custom OBF files for OsmAnd
===========================================

## Setup

1. Make sure the latest version of java is installed.
2. Download OsmAndMapCreator from here: http://download.osmand.net/latest-night-build/OsmAndMapCreator-main.zip
3. Download a PBF file for your area of interest from Geofabrik (http://download.geofabrik.de/) or other source (e.g. activation wiki)
4. Create an OBF folder on your desktop
5. Unzip your OsmAndMapCreator folder to whatever location you want.
6. Place your PBF file inside the OBF folder

## Process

Go to the OsmAndMapCreator folder you created. 
Open the *batch.xml* with Sublime/Atom/the text editor of your choice.
Within the *batch.xml* file find the following lines (should be lines 15-16)

```
<process directory_for_osm_files="/home/..." directory_for_index_files="/home/..." directory_for_generation="/home/..."
		skipExistingIndexesAt="/home/..." indexPOI="true" indexRouting="true" indexMap="true"	indexTransport="true" indexAddress="true">
```

Replace all instances of *"/home/..."* with *"/users/$yourusername/Desktop/OBF"* where $yourusername is your user name on your computer. Save the *batch.xml* file and exit.

Now open your terminal, navigate to your OsmAndMapCreator folder and run the following command in your terminal
```
java -Djava.util.logging.config.file=logging.properties -Xms256M -Xmx2560M -cp "./OsmAndMapCreator.jar:./lib/OsmAnd-core.jar:./lib/*.jar" net.osmand.data.index.IndexBatchCreator ./batch.xml
```

In the end, your OBF file should output to the Desktop/OBF folder. You're done!

## Notes

1. Running this process will take a while and use a lot of memory. For a large file (300MB+) this will take a LONG while. Either content yourself with using your computer for tasks that don't consume a lot of memory, find another computer, or take a break while you're waiting.

2. If you want the process to go faster and have the memory, you can increase the total RAM dedicated to the task. The "-Xmx2560M" line in the specifies 2560M of RAM as the maximum for the task. Increase the number here to allocate more RAM.

## Reference pages

Scripting the process: https://code.google.com/p/osmand/wiki/CreateOfflineMapsForYourself
OsmAndMapCreator walkthrough: http://wiki.openstreetmap.org/wiki/OsmAndMapCreator#Downloading_OsmAndMapCreator


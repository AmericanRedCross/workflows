Querying features in Overpass and editing in JOSM
===========================================

Overpass was giving me errors when I first tried to do this. Here's the workflow I learned.

## Process

1. Go to the Overpass website: https://overpass-turbo.eu/
2. Don't use the Wizard. Instead, type your query directly into the left side of the screen. Model it after the following example:

```
node
  ["fixme"="Location approximate"]
  (4.017699, -15.292969, 13.004558, -6.767578);
  out meta;>;out meta qt;
```
In this example, we are searching for all nodes (as opposed to ways/relations) which have the tag, `fixme=Location approximate`. The search is restricted to a bounding box for the area we are interested in (West Africa). The final line has to do with creating the correct metadata for JOSM to open this properly.

3. Click `Run`. You should see all your nodes show up on the map.
4. Make sure JOSM is open and that you have the remote control enabled.
4. Back in the Overpass query window, click `Export` and then try clicking `JOSM` just in case it works.
5. If/when you get a message that JOSM won't work, go back to the `Export` window and click `raw data directly from Overpass API`. This will download a file called `interpreter`
6. Manually change the file extension of your download to `.osm` and give it a real name. e.g. `interpreter` is renamed `guinea-2mar2016.osm`. I suggest including the area and the date you downloaded the data, for future reference.
7. Open JOSM. Drag and drop the .osm file into the JOSM window.

That should do it. You can make your changes and push them from JOSM to OSM in the normal way.

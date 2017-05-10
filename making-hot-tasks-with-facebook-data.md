
1. Add imagery service to geojson.io

![addService](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/addService.gif)

2. Create outline of imagery extent at geojson.io. Save

![findDrawImagery](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/findDrawImagery.gif)

3. Bring imagery extent into QGIS.
4. Add Facebook data into QGIS. For what we are doing, the values of the data are not importnant. We're using the presence of popupulation to drive where the tasks should be.
5. Use `Raster`>`Extraction`>`Clipper` tool in Raster Menu to clip facebook data to the extent of the imagery. Make sure to set the `clipping mode` to "Mask Layer" and select your imagery extent as your mask. Keep the resolution of the input raster and run the process.![clip population](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/clipper.png)
6. To view the clipped population dataset, go to `Properties`>`Style` and under `Render Type` select `Singleband Grey`. In the "Load min/max values" menu, click the `Min/max` radial butten and then click LOAD. Click OK. ![stylePop](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/render.png). You should now see black pixels for where there are population values.
7. Convert clipped facebook data from raster to vector using `Raster`>`Conversion`>`Polygonize` ![polygonize](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/polygonize.png)
8. You should now have a polygon of the population data.
9. FILTER out all 0 values in your new vector dataset, leaving you with only values greater than 0
10. Overlay administrative areas if necessary
11. Create a Vector Grid using `Vector`->`Research tools`
	- Select your imagery extent as the `Grid Extent`
	- For buildings task in rural area make grid 500m x 500m (.005x.005)
	- For roads tasks make grid 1000m x 1000m (.01x.01)
	- Create grid as polygons
12. Check for existing OSM data by downloading data from [POSM Export Tool](export.posm.io) or [Overpass Turbo](overpass-turbo.eu)
13. If part of your grid has already been mapped `Start Editing` on your grid layer and remove the squares that have already been mapped. Download the "Spatial Querey" plugin to select features that intersect the grid.
14. Using the `Spatial Query` Plugin, SELECT FROM your GRID layer WHERE it INTERSECTS your population vector layer.
15. Save only the selected features from your grid layer.
16. You should be left with a grid where there are no features mapped and there is a population present. ![finalGrid](https://arcmaps.s3.amazonaws.com/share/tasksWalkthrough/cleanTask.png)
17. If possible, clip the cells by admin area to allow for creation of separate tasks.
18. `Save As` a geojson
19. Create new task in [HOTOSM Tasking Manager](tasks.hotosm.org)
20. Upload your gridded geojson and select `Arbitrary Geometries` as the option. This will allow for the squares you've already made to be used as the tasks in the project. 

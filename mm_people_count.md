## Missing Maps People Count Walkthrough

### Getting the data

1. Use the [HOT Tasking Manager](http://tasks.hotosm.org) to update csv - mm_tasks_mmm20yy.csv 
	update task number, task URL, % complete, title, and the date which you updated
	in tasking manager search by Missing Maps and sort by creation date
	Autopopulate the URLS using: =CONCATENATE("http://tasks.hotosm.org/project",A1,"/tasks.json")

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/spreadsheet.png)

	save as .csv


2. Download all tasks using wget.

	IN TERMINAL navigate to your working directory and type "wget -i mm_tasks_mmm20yy.csv"

	For naming conventions download [NameChanger](https://mrrsoftware.com/namechanger/) to remove the 
	number from the end of the filename and move it to the beginning

3. Convert tasks to shapefiles
	IN TERMINAL, use the following to batch convert all jsons in the folder, to shapefile:
	        
	        for f in *.json  
	        do  
	        	filename=${f%.*}  
	        	echo "filename = $filename"  
	        	ogr2ogr -f "ESRI Shapefile" $filename.shp "$f"  
	        done  

4. Download 2015 [WorldPop](http://www.worldpop.org.uk/data/) data for each country that has a task. 

### QGIS Preprocessing

5. Create a new map document. Before adding any data, set the CRS to World_Eckert_IV EPSG: 54012. This is an Equal Area Projection, that we will use to calculate later, the area mapped.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/project_doc.png)

6. Merge all the shapefiles you created together. **Vector>Data Management> Merge shapefiles to one**
	Check the Select by layers in the folder box. Shapeile type is polygon. Input, navigate to the folder and select all the .shp files for the tasks. Ouput, save as mmmYY_tasks_merge.shp

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/merge_tasks.png)

7. Now we need to filter the tasks to only squares that have been completed or validated. Right click on the merged shapefile, select "filter". Filter using "state" IN (2,3)

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/query_tasks.png)

8. Right click on the merge shapefile and "Save As" This will save the filtered shapefile without the incomplete tasks save it as mmmYY_comp_tasks.shp -- be sure to save it in the World_Eckert_IV CRS

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/save_tasks.png)

9. Now we need to remove overlapping tasks, to avoid double counting any areas. Vector>Geoprocessing Tools>Dissolve

	Select the mmmYY__comp_tasks shapefile as the input vector layer, for dissolve field select state. Name the output "may16_comp_tasks_dissolve". This will take a good amount of time to run.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/dissolve.png)

10. Merge all the worldpop data. Otherwise we have to do zonal stats one country at a time. **WARNING** This will take a while, and will take up a large amount of space.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/merge_pop.png)

	Make sure that your WorldPop Rasters are projected into the World_Eckert_IV CRS.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/project_raster.png)

11. Install the Zonal Stats plugin. We'll use this to add up the raster data that falls within a task

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/add_plugin.png)

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/add_zonalstats.png)

### Getting the Count

12. Now you've removed duplicate tasks, and projected all of your data sets, you're ready to run Zonal Stats for each of your countries. 

	Select "Zonal Statistics" from the Raster menu and calculate the sum for each country. This will use your polgon to sum up the WorldPop data that falls within its bounds. Be sure to select a column prefix that will help you recognize from which country the data is coming from.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/zonal_stats1.png)

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/zonal_stats2.png)

13. Your attribute table will now contain the new columns you created, with a sum in each row for the "state" by which you dissolved earlier. You can then sum up these columns in either a spreadsheet or through the field calculator in your attribute table.

	![alt text](https://arcmaps.s3.amazonaws.com/share/people_count/screenshots/count.png)





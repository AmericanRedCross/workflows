QGIS Atlas Techniques
======================

# Basics

### Creating an Atlas Layer

1. Create a shapefile that includes ONLY the features you want to create an atlas of (e.g. only the districts you want maps of)
2. Open a new print composer. Give it a name you can remember, like 'Atlas'
3. Go to the 'Atlas Generation' tab and check the box next to "Generate Atlas".
4. Now set "Coverage Layer" to the shapefile you created above.
5. Under "Output Filename Generation" replace 'atlas' with whatever text you want.
6. Go to 'Item Properties'
7. Check the box next to "Controlled by Atlas"
8. Set the Margin Around Feature to something agreeable. I suggest 25% to leave room for an inset, title, legend, scale bar, etc.

# Advanced

### Setting styles to be different for an atlas feature

If you're styling a layer that uses the same shapefile as your atlas extent, you can style your atlas feature differently. 

This could mean setting a different color for the atlas feature. For instance, you could assign a strong green border to the atlas feature to make it stand out. Alternately, you can apply a style to all the *non-atlas* features. For instance you can mask the the non-atlas districts with partial transparency or complete whiteness.

1. Double click on the layer to open Properties
2. Go to the Style tab
3. Select 'Rule-based' from the options along the top
4. Add two new rules using the Green +
5. Double click on one of these new rules
6. Under "Filter" enter ```$id=$atlasfeatureid```
7. Set the style to whatever you want for the atlas feature style (or set it to empty to show any style underneath)
8. Double click on the other rule
9. Under "Filter" enter ```ELSE```
10. Set the style to whatever you want the non-atlas feature style to be (or set it to a semi-transparent style to show a partial version of any style underneath)

### Setting labels to only show up inside the Atlas feature

1. Enable editing for the features you want to label. For each feature:
2. Create a new field name "centroid" and set its parameters as

```
GeomToWKT(centroid)
```

You should now have fields that reads ```POINT(XX.xxxxxxxx, YY.yyyyyyyy)``` for each feature

3. Save this output
4. Double click on the layer to open Properties
5. Under the label tab, check the box next to "Label this layer with" and click the Expression option. An Expression Dialog will open.
6. Set the following parameter for your labels to appear

```
CASE WHEN intersects($atlasgeometry,GeomFromWKT("centroid")) THEN "YOUR_LABEL_FIELD" END
```

7. Now labels should only appear for this feature when it's within the atlas outline. 
8. Repeat for all features as necessary.

### Creating an inset

Once you've set up your atlas you can create an inset that reflects the current atlas feature. 
You can do many things with this inset. You can draw a box around the atlas map area on an inset map. You can style the inset map so the current atlas feature is highlighted.

1. Load the shapefiles for all the features you want to include in your inset. Make sure to include the atlas shapefile (from #1 above)
2. Turn off all the other layers
3. Apply whatever styles and scale you want to the inset map.
4. If you want to have the current atlas feature styled differently, apply the technique above leveraging the ```$id=$atlasfeatureid```.
5. Load up your Print Composer
6. Create a new map frame. Size it as you want and then position it where you want the inset to be.

*If you want to have the atlas feature highlighted in the inset*

1. Open the Properties dialogue for the shapefile you're building the atlas off of. Go to Style.
2. Use the process explained above under "Setting styles to be different for an atlas feature" to style the atlas feature differently.
3. Now when you rotate through atlases, the inset style will automatically change to reflect the new atlas feature.

*If you want to draw a box around the atlas area*

1. Select your inset map frame within the print composer.
2. Make sure you've already set up your main map
3. Under 'Item Properties' go to "Overviews". Open the menu.
4. Click the green +
5. Select the new **Overview 1** item.
6. Under "Map Frame" select "Map 0". This draws an overview based on the extent of your main map.
7. Under "Frame Style" style the box you're drawing. It can be partially transparent, full, only a border, or anything else you desire.

*Optional*

8. Select an option from the "Blending mode" dialogue to apply a blending effect.
9. Check **Invert Overview** to apply the box style to everything *outside* the box.
10. Check **Center on Overview** to center the inset on the box. **Note**: This cannot be reversed by unchecking the box. You will have to manually re-scale the inset.

*If you're happy with the map scale and style*

1. Go to 'Item Properties' and under "Main Properties" check **Lock layers for map item**.
2. Your inset will now stay the same even as you turn off the inset layers and turn on your map layers.

# Notes

1. The atlas ID field is invisible to you and hard to work with. If you use formulas that work off the atlas ID then you need to use the same shapefile or a shapefile with the same features. This ensures the IDs align. For instance, if the inset highlights a district based on the atlas ID (to show where the map is), it needs to highlight the districts from a layer file referencing the same shapefile as the Coverage layer file. 

<img src="https://cloud.githubusercontent.com/assets/1583376/8830498/7dc3d4fe-306a-11e5-846f-a62e9151e722.jpg" alt="correct map inset" style="width:283px;"/>

Otherwise the districts IDs won't align ("2" for the coverage layer will indicate a different district in the Inset). This will cause the inset to highlight separate districts.

<img src="https://cloud.githubusercontent.com/assets/1583376/8830497/7dc366c2-306a-11e5-83bf-9ba4dbb572cf.jpg" alt="incorrect map inset" style="width:283px;"/>

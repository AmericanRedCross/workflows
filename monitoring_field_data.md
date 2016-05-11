## Fieldwork: Tips for monitoring data

Best practices learned from West Africa, courtesy of Ivan Gayton.

### Daily checks are important

It's a good idea to map the ODK output data in QGIS daily, as it allows you to check several aspects of quality that the spreadsheet view does not. For example, you can tell if a point is in the wrong place (i.e. volunteer completed the survey from a completely different area, which I've seen once in the data), or if a given village has a sous-village name, but there's no corresponding sister sous-village nearby (sous-village should only really appear if there is more than one group of houses with the same village name, otherwise that field should be 995).


### Process for viewing the data in QGIS

1. Download the CSV from the OMK server.
2. Copy the data into a spreadsheet that contains a sheet with the volunteer registration data.  Leave two columns blank on the left.
3. In the two left-most columns, us a vlookup formula to correlate the device ID to the volunteer name and location (for example, Gneka Gouhara in Lola).  that makes it easy to figure out who's made mistakes and need support, both at the individual level and the team level.
4. Re-export the resulting data, which now includes volunteer names and base location/teams, as CSV.
5. Import the data as a CSV layer in QGIS.

Once this is done, you can add to or re-do the CSV as often as you like.  Provided you don't change the column order, QGIS will simply display the updated data without re-importing.

6. We then display the data in a half-dozen duplicated layers (same data source, but different layer styles and labelling), including a view categorized by sous-prefecture, another categorized by district, another by volunteer team, and several different layers that display different columns as labels (allows me to quickly turn on or off various different labels by activating or deactivating the relevant layers)

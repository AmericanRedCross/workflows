- It's possible to manually install plugins
    - https://josm.openstreetmap.de/wiki/Help/Preferences/Plugins#Manuallyinstallingplugins
    - https://josm.openstreetmap.de/wiki/Help/Preferences#Windows
    - https://josm.openstreetmap.de/wiki/Help/Preferences#MacOSX
- grab the plugin files here: https://josm.openstreetmap.de/wiki/Plugins

- you can grab the ESRI satellite basemap tiles as an mbtiles for an area with
```
tl copy -z 19 -Z 19 -b '{{lng-min}} {{lat-min}} {{lng-max}} {{lat-max}}' 'https://a.tiles.mapbox.com/v4/digitalglobe.0a8e44ba/{z}/{x}/{y}.png' mbtiles://./{{myFileName}}.mbtiles
```
- you can open mbtiles in JOSM with the `mbtiles` plugin
- you can get a layer to show up as a visible purple box (instead of the subdued grey) in JOSM by converting it to a gpx using the `editgpx` plugin

## Issues and things to watch out for

Here, the building attributes were added to a node and not to the “closed way” or polygon that represent the complete boundary of the building.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue01.png)

Here, a building was split into multiple buildings using multiple line segments and not actually divided into separate polygons.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue02.png)

The key-value pairs used to tag features should be taken from the OSM map features wiki.

Here, a building has been tagged shop=Barbar. This should be shop=beauty or shop=hairdresser. Note: Values (unless a name) should be all lowercase with no spaces.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue03.png)

This is an incorrect tag. 
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue04.png)
The correct way to tag would be this.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue05.png)

Here, there are overlapping and duplicate buildings. The iD editor will hide features at low zoom levels. Users should check the lower right corner of their screen where the editor displays the number of hidden features. Before editing, users should zoom in until the number of hidden features is 0.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue06.png)
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue07.png)

In the areas already surveyed there are multiple buildings with the same house number. Field Papers should be used to take detailed notes about features that need to combined, features that need to be split, missing features, and other problems with the existing data.
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue08.png)


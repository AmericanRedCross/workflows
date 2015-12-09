## Project \#1391 - MissingMaps: Moghbazar, Dhaka

For this [task](http://tasks.hotosm.org/project/1391) tracing in Dhaka, Bangladesh there are two scenes available. Through the MapGive project, the Humanitarian Information Unit (HIU) of the U.S. Department of State is providing the OpenStreetMap community access to updated satellite imagery services to help assist with humanitarian mapping.

2015-03-22 `http://hiu-maps.net/hot/1.0.0/dhaka-22mar2015-flipped/{zoom}/{x}/{y}.png`

2015-11-07 `http://hiu-maps.net/hot/1.0.0/dhaka-07nov2015-flipped/{z}/{x}/{y}.png`

The November imagery is a little bit more clear but both imagery sources should be used. Both are off-nadir (captured at an angle instead of directly overhead resulting in the slightly offset appearance in which you can see the sides of buildings). It is important to:

1. Trace the building use the outline of the roof and then shift the feature to line up with the ground-level footprint of the building.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/moghbazar-tracing-guide/off-nadir-correction.png)

2. When tracing around tall buildings, switch between the two scenes. The direction of off-nadir is opposite, so shorter adjacent buildings that are hidden in one scene will be visible in the other.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/moghbazar-tracing-guide/dhaka-22mar2015.png)
![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/moghbazar-tracing-guide/dhaka-07nov2015.png)

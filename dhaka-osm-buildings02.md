## Tracing buildings in Dhaka, Bangladesh
#### Complex rooftops and off-nadir imagery \#2

- Let's trace the building in the center of the image.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings02/dhaka-osm-buildings02-a.png)

- We might trace it like this. But go back and take a closer look at the imagery. This isn't four buildings, only one!

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings02/dhaka-osm-buildings02-b.png)

- The roof isn't completely flat, but we are looking at one building. The actual footprint of the building is closer to this shape. There's another effect that we need to take into account. Notice how you can see half of the sides of the buildings. This satellite imagery is off-nadir. It was taken at an angle and not from directly above. Tall features in the image will not have their outline at ground level match their outline at roof level. It's easier to trace the roof because we can see the entire thing. But we want the polygon to match the ground location of the building.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings02/dhaka-osm-buildings02-c.png)

- After tracing the outline using the roof we need to shift the polygon so that the corner matches the ground-level corner of the building we can see. It can be difficult. In this image the corner is hidden by shadows and the adjacent building. But we can make a pretty good guess.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings02/dhaka-osm-buildings02-d.png)

- Let's look at another imagery source. This imagery still slightly off-nadir, but much less. Note that it's off-nadir in a different direction. Instead of seeing the upper and left sides we see the lower side. Our tracing matches this other imagery source pretty well.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings02/dhaka-osm-buildings02-e.png)

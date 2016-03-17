## Tracing buildings in Dhaka, Bangladesh
#### Complex rooftops and off-nadir imagery

- Let's trace the circled building in the center of the image.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-a.png)

- We might trace it like this...

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-b.png)

- Let's look at another imagery source. The outline we've traced doesn't match anything! What's going on?

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-c.png)

- Taking a closer look at our original imagery we see that what we traced around a shadow on the roof from a small raised structure and also left out a section of the roof that is slightly lower.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-d.png)

- The actual footprint of the building is closer to this shape. There's another effect that we need to take into account. Notice how you can see half of the sides of the buildings. This satellite imagery is off-nadir. It was taken at an angle and not from directly above. Tall features in the image will not have their outline at ground level match their outline at roof level. It's easier to trace the roof because we can see the entire thing. But we want the polygon to match the ground location of the building.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-e.png)

- After tracing the outline using the roof we need to shift the polygon so that the corner matches the ground-level corner of the building we can see. It can be difficult. In this image the corner is hidden by shadows and the adjacent building. But we can make a pretty good guess.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-f.png)

- Let's look back at our other imagery. This imagery still slightly off-nadir, but much less. Note that it's off-nadir in a different direction. Instead of seeing the upper and left sides we see the lower side. The polygon we traced lines up much better.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-buildings01/dhaka-osm-buildings01-g.png)

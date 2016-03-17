## Tracing buildings in Dhaka, Bangladesh
### Off-nadir imagery

- Satellite imagery is sometimes captured off-nadir. This means it was captured at an angle instead of directly overhead resulting in the slightly offset appearance. You'll be able to see the sides of tall buildings. Tall features in the image will not have their outline at ground level match their outline at roof level. It's easier to trace the roof because we can see the entire thing. But we want the polygon to match the ground location of the building. After tracing the building using the outline of the roof you'll want to then shift the feature to line up with the ground-level footprint of the building.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-offnadir/dhaka-osm-offnadir-a.png)

- Imagery can be off-nadir in any direction. These two images are of the same place but the direction of off-nadir is opposite, so shorter adjacent buildings are mostly hidden in one scene but visible in the other.

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-offnadir/dhaka-osm-offnadir-b.png)

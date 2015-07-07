# Dhaka Data4Action

## Workflow
- Check satellite imagery for areas where buildings can be traced but are not yet included in OSM.
- Conduct a field survey. (*It may be easier to do the field work in two stages. A first stage using only Field Papers to correct and finalize the building footprints. And a second stage, using both Field Papers to collect points of interest (shops inside buildings, etc.) and the OpenMapKit app to survey the buildings.*)
  - Use the OpenMapKit app for existing buildings (contact the American Red Cross GIS team to setup the survey).
  - Use Field Papers for errors and missing details such as:
    - a feature traced as a single building should actually be multiple buildings
    - a feature traced as multiple buildings should actually be a single building
    - a building is missing
    - a road is missing
    - the points of shops and amenities
- Upload completed OpenMapKit forms and work with the American Red Cross GIS team to add the data to OSM.
- Use JOSM to create/upload data recorded on Field Papers.
- Check the data in OSM for incorrect tagging, etc.


## Tagging

- key is **building**
  - values are { yes | construction | residential | commercial | industrial | mosque | hospital | school | public }
- key is **building:use** >> *Use this tag if building=mixed (multi-purpose) to provide additional detail. Type a semicolon separated list with no spaces (for example building:use=residential;commercial).*
  - values are { residential | commercial | industrial | place_of_worship | education | government }
- **building:levels** >> *Number of floors. When the top floor(s) are smaller than the street-level building footprint use your best judgement when deciding whether to count. Are they part of the structure or secondary additions? Are they close to the same area or only a small portion?*
  - value should be an integer number { 1 | 2 | 3 | ... }
- key is **building:condition**
  - values are { poor | average | good }  
- key is **name**
  - If the building has a posted name you can include it.
- key is **addr:housenumber**
  - Holding number. Capitalize all letters.
- key is **addr:street**
  - Don't abbreviate (for example, use "Road" and "Lane" NOT "Rd" and "Ln").
  - Use title case. Capitalize the first letter of each word.

Note: If a building has only a single use, the following tags can be used on the building polygon. Otherwise, these tags should be used on points added inside the outline of the building.

- **amenity**
  - { atm	| bank	| cafe	| clinic	| college	| community_centre	| dentist	| doctors	| fast_food	| hospital	| library	| pharmacy	| place_of_worship	| police	| post_office	| recycling	| restaurant	| school }
- **shop**
  - *Many times should be a node placed inside a building polygon*
  -	convenience *(small subset of items you would find in a supermarket)*
  -	general *(assorted items, if it sells food use shop=convenience)*
  -	farm *(shop or roadside stand focused on selling freshly harvested farm produce)*
  -	bakery *(bread)*
  -	butcher *(meat)*
  -	confectionery *(sweets or candy)*
  -	pastry *(baked sweets like cakes, biscuits, pies)*
  -	clothes
  -	fabric
  -	jewelry
  -	leather
  -	shoes
  -	tailor
  -	chemist *(personal hygiene, cosmetics, household cleaning supplies, drugs. For prescription drugs use amenity=pharmacy)*
  -	hairdresser
  -	hardware *(building supplies like nails, screws, paint, etc)*
  -	paint
  -	trade *(building supplies like timber/wood, cement, etc)*
  -	houseware *(pots, pans, kitchenware, small appliances)*
  -	bed *(mattresses and other bedding products)*
  -	furniture
  -	electronics
  -	copyshop *(photocopying, printing services)*
  -	computer *(electronics shop selling only computers)*
  -	mobile_phone *(electronics shop selling only mobile phones and accessories)*
  -	mobile_recharge
  -	bicycle
  -	car
  -	car_repair
  -	car_parts *(selling auto parts, auto accessories, motor oil, car chemicals, etc)*
  -	books
  -	gifts *(selling gifts, greeting cards, tourist gifts, souvenirs)*
  -	stationery *(paper, office supplies)*
  -	funeral_directors *(providing services related to funeral arrangements)*
  -	musical_instrument

## Additional tagging notes

- Cemeteries should be tagged landuse=cemetery
- Dense slum areas of small, close together structures can be tagged as landuse=residential instead of trying to map individual buidings.
- Don't include the same tags on two objects. [One feature, one osm element](http://wiki.openstreetmap.org/wiki/One_feature,_one_OSM_element)
  - For example, if a building is tagged as a mosque do not also include a point within the building tagged as a mosque.
  - For example, if school grounds are mapped as amenity=school and the building(s) are mapped as building=school only include the name of the school on the outermost feature (the grounds) and not on both.

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

If not a name, values in tags should be all lowercase and have no spaces. This should be landuse=open_space. Another issue is that there are [less than 5 uses](https://taginfo.openstreetmap.org/tags/landuse=open_space) of the open_space value. Depending on the feature consider using leisure=park ([over 465,000 uses](https://taginfo.openstreetmap.org/tags/leisure=park)) or leisure=common ([over 48,500 uses](https://taginfo.openstreetmap.org/tags/leisure=common)) or landuse=brownfield ([over 44,500 uses](https://taginfo.openstreetmap.org/tags/landuse=brownfield)).

![](https://raw.githubusercontent.com/AmericanRedCross/workflows/master/images/dhaka-osm-issue09.png)

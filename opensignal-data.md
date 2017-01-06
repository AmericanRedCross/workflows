# Mapping cell phone signals with OpenSignal

This past spring/summer, over 100 Red Cross volunteers conducted field mapping in the border regions of Guinea, Liberia, and Sierra Leone. In addition to the actual mapping, we also asked the volunteers to record their GPS tracks each day, and we set their phones to automatically collect cell signal strength data using OpenSignal, an app which crowdsources this information.

Connectivity is very poor in this region, and volunteers often had to travel several hours to different cities if they wanted to be able to use their phones to make calls. By collecting signal strength data, we hope to make it easier for people to know where there is a useable cell phone signal.

Now that the fieldwork has finished, we've had a chance to start going through all this data to see what connectivity looks like in West Africa. We haven't come across much about working with OpenSignal data, so this post documents our workflow for using the data, the challenges we had, and our results.


## Getting, merging, and cleaning the data

For this project, we used 14 Samsung Galaxy S5 phones and about 100 Blu Advance 5.0 phones. We've tried a lot of different phones in the field, and the Blu's are our favourite so far - cheap, hardy, easy to use, and they have a reliable GPS signal.

We loaded OpenSignal onto all of the phones before the fieldwork began, then downloaded the data at the end of the project, following the [instructions from OpenSignal](https://opensignal.com/blog/2015/06/08/updated-data-collection-format/).

OpenSignal generated three types of CSV files: wifi, speedtests, and cell signals:

![] (https://arcmaps.s3.amazonaws.com/share/blog-pictures/file_types.png)

 Since we only care about the cell signal strength, I put all these into a folder and then ran a quick command in Terminal to merge them:

 `cd [folder with .csv files]
  cat *.csv > merged.csv`

The resulting file was a little strange. First, the individual files didn't have consistent header rows - some exports had considerably more columns, and the columns didn't match up between the different formats; the Samsung and Blu phones exported very different formats. I split the files by phone type (Samsung vs Blu) and concatenated the two batches separately, then combined them and made the columns line up. This worked out.

The next step was figuring what all this data means. [OpenSignal's handy post](https://opensignal.com/blog/2015/06/08/updated-data-collection-format/) explained almost everything we needed to know, with one exception: signal strength was measured on different scales and had to be converted into a consistent scale. More on this below.

Finally, I cleaned up a few parts of the data:

1. Timestamps are given in Linux/Unix epoch format, measuring the number of milliseconds since 1970. I converted these to a human readable date in Microsoft Excel so I could check how often OpenSignal was recording data. I've read that Microsoft Excel date formats are slightly different depending on whether you're using Windows/Mac OS, but on my Mac I actually needed to use the Windows conversion. The formula for this is:

`=(((X/1000)-(T*3600))/86400)+(DATEVALUE("1-1-1970") - DATEVALUE("1-1-1900"))`

where X is the cell with the time in epoch and T is offset from GMT time, in hours. You'll need to change the format of those cells to a date, as well.

2. Location inaccuracy. The maximum location inaccuracy was almost 5 km. I discarded any records with a location inaccuracy greater than 1000 metres. This seems like a very high number to me, but it eliminated almost a quarter of my dataset, dropping it from 200,000 records down to 150,000.

3. RSSI (Received Signal Strength Indicator) measures the signal strength. HOWEVER, it's measured differently depending on the network type. For EDGE, GPRS, HSPAP, and sometimes HSDPA and HSPA, it is measured on a scale of -1 to 31. On other HSDPA and HSPA networks, it's measured in dBm, on a scale of -113 to -51.

There were other instances where we had "unknown" and "out of service" networks with an RSSI of 99. I wasn't sure if this was code for "no signal", or if it meant that RSSI was being measured on yet another scale - the internet tells me that the RSSI max is 99 on Cisco equipment. These records added up to only 1% of the data so I just discarded them.

I converted the RSSI column into dBm in Excel in one fell swoop:
`=IF(RSSI<(-50),RSSI,IF(RSSI>31,"",(RSSI*2-113)))`

This leaves values already measured in dBm, converts those on the -1 to 31 RSSI scale (the formula is: `RSSI*2 - 113 = dBm`), and returns an empty value for anything above 31.

When I put this data into GIS, I coded the dBm values into signal strength categories. I found several different scales for this, so I ended up with the following "compromise":

-113 to -101: Very poor
-100 to -86: Weak
-85 to -71: Good
-70 to -51: Excellent

- Lat/long: Because we set the phones up in the US, I discarded any lat/long pairings taken outside of West Africa.

This gave me a clean dataset ready to be saved as a Windows CSV and loaded into GIS.

A few comments about this data:

1. It would be really helpful if OpenSignal data contained the IMEI number of the phone. This would let me sort through the data and group by phone, to better understand how much data was recorded on a phone, which might be split into several files.

2. Data cleaning would have been easier if OpenSignal data was set to export with consistent column headers.

3. The number of records seems really low. With over 100 phones being used for weeks and weeks, I would expect more than 150,000 usable records. This didn't make sense so I calculated the interval between records. This didn't make any sense to me - there wasn't a consistent interval between pings, and it looks like several pings were recorded at the exact same time, then there would be a huge gap (hours, days) until the next ping. I didn't find any documentation about this, so I can't tell if this means that OpenSignal wasn't looking for a signal (and why not?), or if there was no signal at all (which is still important to record), or if perhaps the phone was overwriting old data (but the file sizes didn't seem to have a cut-off point, so this is unlikely). This seemed to be a major problem with using OpenSignal; the data would have much more value if we had a record every 10 mins, or something like that. More on this later.

The cleaned dataset (as a shapefile) and QGIS style file are [here](https://www.dropbox.com/s/e4piya18hburba0/opensignaldata.zip?dl=0) in case anyone wants to play with it.


## GIS analysis... and data issues

I loaded the CSV file into GIS and converted it into an equal-area projection (to enable accurate distance/area calculations).

Again, the data look very sparse compared to the amount of volunteers and time spent in the field. The image below shows the OpenSignal data overlaid on GPX tracks collected by volunteers (shown in grey) for the West African region. The OpenSignal data covers some main highways across the region and some clusters in certain cities, but it's extremely sparse compared to what I was expecting.

![] (https://arcmaps.s3.amazonaws.com/share/blog-pictures/signal_strength.png)

The settings on the OpenSignal app explain, "Data is collected when the app is open and at a low rate when it is closed (around 10 signal readings per hour)."

That's not what I see in the West Africa data. The snippet below contains data from a few different files. In each of these files, a phone collects data briefly when set up in late March... then nothing until a month later, at the end of April. When the phones are logging data, they are doing so at the expected rate of about 10x per hour... it's just that there are huge gaps between the readings. I'd love to know more about why this is and if there is something we can correct, or if it's a bug that can (or has) been fixed.

![] (https://arcmaps.s3.amazonaws.com/share/blog-pictures/timestamps.png)

## Next steps

Next steps for the data involve turning the OpenSignal data into a raster (ie pixellated) grid that covers the area, turning it into a full-coverage surface rather than a collection of points. There isn't enough data to do this comprehensively for the region, as we'd hoped, but we can analyze local areas where the dataset is larger.

To do this, we zoomed in to an area in the Eastern Province of Sierra Leone with a high density of signal recordings. We took the RSSI values for these recordings and then performed [kriging](http://www.qgistutorials.com/en/docs/interpolating_point_data.html) using the inverse distance weighting method. What this means: we have a set of points and we want to fill in the gaps between them to predict what the cell signal strength will be in other areas nearby. When doing this, we set a distance limit on how far away the kriging will examine. Too small, and we won't learn that much. Too large, and the results won't be very accurate. Even with an appropriate distance limit, predictions won't be perfect because we aren't factoring in topography or other things that might affect signal strength. But this is still enough to help understand the gaps in the data for a local area. The output from the kriging is a grid of cells, each of which has a predicted RSSI value. This helps us to understand connectivity "hotspots" in the local area.

![] (https://arcmaps.s3.amazonaws.com/share/blog-pictures/kriging.png)

Distributing maps like these would be helpful for local Red Cross volunteers and community members in general, who often end up traveling between cities in order to make a phone call.

These data could be combined with population datasets like [WorldPop](http://www.worldpop.org.uk/) to examine populations groups with (and without) access to cell connectivity.

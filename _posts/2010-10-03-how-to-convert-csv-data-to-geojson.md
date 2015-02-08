---
title: How to convert CSV data to geoJSON
author: Andrew
layout: post
permalink: /how-to-convert-csv-data-to-geojson/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:1:{i:0;s:3:"486";}'
categories:
  - Programming
---
A few weeks ago [I posted about some things I&#8217;ve been reading][1] on how to incorporate data on a map for the web using open-source OpenLayers. While other work has kept me away from making substantial progess on the maps, I have made some steps towards converting data into geoJSON format for use in these types of web applications. The solution I have isn&#8217;t exactly elegant since it is very specific one dataset but it works and should be adaptable.

I&#8217;m new to using [github][2] for code but I have posted the code for this script up there to share with whoever can make something useful of it. You can [download the Python script][3] to convert CSV (with lat/long coordinates) to geoJSON or [clone the .git repository][4].

Below I post the body of the Python script for comments if anyone should pass this way with suggestions for improvements.

<pre class="brush: python; title: ; notranslate" title="">import csv

# Read in raw data from csv
rawData = csv.reader(open('sample.csv', 'rb'), dialect='excel')

# the template. where data from the csv will be formatted to geojson
template = \
    ''' \
    { "type" : "Feature",
        "id" : %s,
            "geometry" : {
                "type" : "Point",
                "coordinates" : ["%s","%s"]},
        "properties" : { "name" : "%s", "value" : "%s"}
        },
    '''

# the head of the geojson file
output = \
    ''' \
{ "type" : "Feature Collection",
    {"features" : [
    '''

# loop through the csv by row skipping the first
iter = 0
for row in rawData:
    iter += 1
    if iter &gt;= 2:
        id = row[0]
        lat = row[1]
        lon = row[2]
        name = row[3]
        pop = row[4]
        output += template % (row[0], row[2], row[1], row[3], row[4])
        
# the tail of the geojson file
output += \
    ''' \
    ]
}
    '''
    
# opens an geoJSON file to write the output to
outFileHandle = open("output.geojson", "w")
outFileHandle.write(output)
outFileHandle.close()
</pre>

 [1]: http://www.andrewdyck.com/mapping-data-on-the-web-using-mapbox-openlayers/
 [2]: http://github.com
 [3]: http://github.com/andrewjdyck/csvToGeoJSON/blob/master//csvToGeoJSON.py
 [4]: https://andrewjdyck@github.com/andrewjdyck/csvToGeoJSON.git
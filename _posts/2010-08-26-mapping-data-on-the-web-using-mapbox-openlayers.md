---
title: 'Mapping data on the web using Mapbox &#038; OpenLayers'
author: Andrew
layout: post
permalink: /mapping-data-on-the-web-using-mapbox-openlayers/
openid_comments:
  - 'a:1:{i:0;s:4:"2032";}'
categories:
  - Personal
tags:
  - data
  - javascript
  - mapping
  - visualization
---
  




This post is mostly a note to myself covering some of the research I&#8217;ve been doing over the past day with mapping data for the web. I&#8217;ve found a number of really nice interactive mapping tools that I&#8217;m looking into including [Mapbox][1], [OpenLayers][2], [Polymaps][3] and [Google Maps API][4]. Although they look nice, I&#8217;ve been avoiding Flash based tools. Mostly because I don&#8217;t know Actionscript and also because I think html5/javascript is where technology is headed in the near future.

**Background**

Over the past two years, the [Global Ocean Economics Project][5] that I&#8217;ve been working for has generated/collected some interesting global data. The data is organized very simply into a longitudinal format with countries as the cross-sectional identifier. The [head of this data][6] would look something like this:

<table>
  <tr>
    <td>
      Country
    </td>
    
    <td>
      Year
    </td>
    
    <td>
      Data
    </td>
  </tr>
  
  <tr>
    <td>
      Canada
    </td>
    
    <td>
      2000
    </td>
    
    <td>
      100
    </td>
  </tr>
  
  <tr>
    <td>
      Canada
    </td>
    
    <td>
      2005
    </td>
    
    <td>
      200
    </td>
  </tr>
  
  <tr>
    <td>
      USA
    </td>
    
    <td>
      2000
    </td>
    
    <td>
      200
    </td>
  </tr>
  
  <tr>
    <td>
      USA
    </td>
    
    <td>
      2005
    </td>
    
    <td>
      400
    </td>
  </tr>
</table>

For now I&#8217;ll ignore the time element of the data and focus simply on displaying a cross-section on a global map. I&#8217;ll consider displaying time-series on the map later.

**Mapbox**  
This appears to be a strong contender for my final product although it appears to be geared towards an audience a little higher in terms of technical efficiency.

I was first tipped off to Mapbox after falling for the data displays on the new [World Bank data site][7]. The map on the front page gets its message across while remaining very clean and simple. After looking at this page&#8217;s source code I saw that they called scripts from mapbox.com so I checked it out and after reading a little on that site I was able to produce this:

<div id="map" style="width: 500px; height: 300px">
</div>

The code necessary to use the [World Light][8] tileset above can be [downloaded here][9]. Also at that link are instructions for working with [Drupal][10] and Google Maps API.

The next step is to add data and make it look more like [this app from the National Democratic Institute][11].

**OpenLayers**  
OpenLayers is an open source javascript library for making &#8216;slippy&#8217; maps. I believe it is the brawn behind Mapbox, however, the documentation is a little vague for my liking and it will take some more time before I can comment on this further.

**Polymaps**  
This looks to be very nice. Good set of examples and the documentation seems useful. It&#8217;s also nice to see that they are dedicated to using SVG, which will likely be very useful in the future of the web. As a user of [Inkscape][12], I&#8217;m happy to see more support for SVG on the web. For the time being I&#8217;ve decided not to pursue Polymaps any further because I fear hitting some walls in terms of SVG being incompatible with some browsers (I&#8217;m looking at you IE6!).

**Google Maps API**  
Why leave Google to last? Normally the GOOG would be the first place I look, but I was under the impression that Google Maps was Flash only. Turns out that I was prematurely turned off since they do have non-flash version, however, at the moment I feel that I&#8217;ve made more headway with other options so I&#8217;ll stick to that.

**future research**  
At the moment all the data files are static so there is no need to concern myself with connecting the map to an analysis engine like Stata (or R via Rapache). However, in the future I&#8217;d like to investigate how to make such interactive maps dynamic in that they take output from Stata scripts and plot them on the web. This could be done automatically to do something like:

  1. Download monthly crime data
  2. Run some regressions
  3. Report the results on an interactive map

**Done for now**  
Like I said earlier, this is mostly a note to myself to collect some links and my progress researching this topic. But, if you happen to read all the way through this and have any comments or can suggest a new direction for me to take, please do so below.

 [1]: http://mapbox.com/
 [2]: http://openlayers.org/
 [3]: http://polymaps.org/
 [4]: http://code.google.com/apis/maps/index.html
 [5]: http://feru.org/goep/
 [6]: http://codeandculture.wordpress.com/2010/08/25/heads-or-tails-of-your-dta/
 [7]: http://data.worldbank.org
 [8]: http://mapbox.com/tileset/world-light
 [9]: http://mapbox.com/documentation/adding-tiles-your-site
 [10]: http://www.drupal.org
 [11]: http://afghanistanelectiondata.org/data
 [12]: http://www.inkscape.org/
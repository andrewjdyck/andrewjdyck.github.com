---
title: Getting javascript to run in a WordPress blog entry
author: Andrew
layout: post
permalink: /getting-javascript-to-run-in-a-wordpress-blog-entry/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
categories:
  - Personal
tags:
  - javascript
  - Wordpress
---
It&#8217;s not as easy as it looks to get javascript to run from inside a WordPress post. [For a recent post][1], I wanted to run a one-off javascript so I didn&#8217;t want to change the header.php file in my theme. Instead I found [this info on the WordPress codex][2] on how to call javascript from inside the <body> tags. 

Also the javascript that I was originally working with used

<pre class="brush: xml; title: ; notranslate" title="">&lt;body onload="init()"&gt;
</pre>

to start the javascript when the page loaded but this wouldn&#8217;t work from a WordPress blog entry. So I had to change my javascript from:

<pre class="brush: jscript; title: ; notranslate" title="">function init() {
something();
goes();
here();
}
</pre>

to:

<pre class="brush: jscript; title: ; notranslate" title="">window.onload = function init() {
something();
goes();
here();
}
</pre>

and then I call the init() function in my blog post using:

<pre class="brush: xml; title: ; notranslate" title="">&lt;script type="text/javascript"&gt;
init();
&lt;/script&gt;
</pre>

**\*Important\***  
I can to change my WordPress user settings to disable the visual text editor since it was adding/stripping various parts of the html and breaking it.

 [1]: http://www.andrewdyck.com/mapping-data-on-the-web-using-mapbox-openlayers/
 [2]: http://codex.wordpress.org/Using_Javascript#Javascript_in_Posts
---
title: First shot at grabbing data from web APIs using Stata
author: Andrew
layout: post
permalink: /first-shot-at-grabbing-data-from-web-apis-using-stata/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:2:{i:0;s:3:"932";i:1;s:3:"977";}'
categories:
  - Programming
tags:
  - API
  - data
  - Stata
---
I love the new World Bank data site. The site makes finding and downloading data from the World Development Indicators very easy. But, I dream of searching the World Bank databases and downloading datasets directly into Stata all without leaving my Stata terminal. 

The World Bank offers an API for it&#8217;s data that has already been[ incorporated into a package for R][1]. The package uses the API to download XML data and parses it into a dataframe. This can be done in R because there is [a nice XML package for R][2] to do the heavy lifting but no such package yet exists for Stata. The API can also serve up data as a JSON object, but that cannot be easily imported into Stata either.

So, how to get an XML or JSON object into Stata? First off, I think that parsing JSON is the way to go since although the World Bank supports both XML and JSON, some other APIs only return JSON and wouldn&#8217;t it be great if Stata could access many web data APIs? If you think XML would be a better/easier route to go, please let me know in the comments.

**What&#8217;s a JSON object?**  
[JSON][3], which stands for JavaScript Object Notation, is an often used data format on the web. It is appears as a string. For example:

<pre class="brush: jscript; title: ; notranslate" title="">"[{"firstName":"John","lastName":"Smith","age":25,"address":{"streetAddress":"21 2nd Street","city":"New York","state":"NY","postalCode":"10021"},"phoneNumber":[{"type":"home","number":"212 555-1234"},{"type":"fax","number":"646 555-4567"}]}]"
</pre>

So compact! It saves on download size (and processing time for larger datasets) but looks a little messy so most JSON parsers will also express a JSON string in &#8220;pretty&#8221; notation which looks like:

<pre class="brush: jscript; title: ; notranslate" title="">[
 {
     "firstName": "John",
     "lastName": "Smith",
     "age": 25,
     "address":
     {
         "streetAddress": "21 2nd Street",
         "city": "New York",
         "state": "NY",
         "postalCode": "10021"
     },
     "phoneNumber":
     [
         {
           "type": "home",
           "number": "212 555-1234"
         },
         {
           "type": "fax",
           "number": "646 555-4567"
         }
     ]
 }
]
</pre>

Here you can see that a JSON object can be multi-dimensional. Stata requires data to be square so before we can get a nice tidy &#8220;json.dta&#8221; file there will need to be some parsing of the json string.

**Reading data from an API in Stata**  
Stata is a great program for data analysis but turns out it&#8217;s not the greatest web browser. It does not handle redirects well, I&#8217;d guess for security, so my plans for making a Stata Twitter client (with [Jeffrey Horn][4]) will probably be on hold until we can figure out a way to get around this limitation or something new is introduced in a Stata update. 

*If you want to see the problem with Twitter redirects, try using the url &#8220;http://search.twitter.com/search.json?q=@Stata&#8221; with the Mata program I include later in the post.*

**Parsing pretty(ish) JSON with Stata**  
So far I have two methods in mind for reading JSON data. The first uses Mata commands to read the string into Mata&#8217;s memory and the other uses the command -intext- which will read the string directly into Stata. I&#8217;m partial to the first method because it involves reading JSON data into an associative array that can be munged for use on many other websites. <del>The downside is that, as far as I can tell, associative arrays were introduced in Stata 11.1 so users who haven&#8217;t upgraded to the latest version wouldn&#8217;t be able to use it.</del>

That said, I&#8217;m a long way off from getting JSON data into a .dta file so I&#8217;m very open to ideas and help. So far, I have written a quick mata program that will read json data from a url and display the (not quite pretty) formatted data in the terminal. The rudimentary code is:

<pre class="brush: perl; title: ; notranslate" title="">mata
void pretty_json(string scalar url)
{	
	b = fget( fopen( url, "r" ) )
	b = subinstr( b, `"{"',`"{\n"')
	b = subinstr( b, `"["', `"[\n"')
	b = subinstr( b, `",""', `",\n""')
	b = subinstr( b, `",["', `",\n["')
	b = subinstr( b, `""}"', `""\n}"')
	b = subinstr( b, `",{"', `",\n{"')
	b = subinstr( b, `":{"', `": {"')
	b = subinstr( b, `"},"', `"\n},\n"')
	printf(b)
}
</pre>

Then test it out on World Bank data for Brazil&#8217;s GNP between 1960:1970:

<pre class="brush: perl; title: ; notranslate" title="">url = "http://api.worldbank.org/countries/br/indicators/NY.GNP.PCAP.CD?date=1960:1970&format=json"
pretty_json(url)
</pre>

You should see the data string is now in lines instead of a character string in your terminal. This could be written to a text document, imported to Stata using -intext- and cleaned with some regex skills. Probably the fastest way to get web api data into Stata the main drawback is that it doesn&#8217;t allow for much interaction with the API and one would need to know the url first. The World Bank API has search functionality and I&#8217;d love for a Stata World Bank data module to allow the user to search the database, choose a series to download and then import that data.

Any comments from fellow Stata users out there would be greatly appreciated. My progress on this topic is in a [git repository on github][5] if you want to watch or branch it.

**Update:** *[@Stata][6] on Twitter sent my a direct message informing me that associative arrays were actually introduced during Stata 10&#8217;s lifetime so it&#8217;s only pre-Stata 10 users that wouldn&#8217;t be able to use ado files that involve associate arrays.*

 [1]: http://cran.r-project.org/web/packages/WDI/index.html
 [2]: http://cran.r-project.org/web/packages/XML/index.html
 [3]: http://en.wikipedia.org/wiki/JSON
 [4]: http://www.failuretorefrain.com/jeff/
 [5]: https://github.com/andrewjdyck/statajson
 [6]: http://twitter.com/#!/Stata
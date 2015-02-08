---
title: Random conversion of imported data to factors in R
author: Andrew
layout: post
permalink: /random-conversion-of-imported-data-to-factors-in-r/
categories:
  - Software
tags:
  - Programming
  - R
  - statistics
---
While getting extremely frustrated trying to import a simple dataset into R today I stumbled upon a post by <a href="http://erehweb.wordpress.com/2009/05/26/r-and-data/" target="_blank">Erehweb</a> who sarcastically dissects the difficulty of importing numeric data into R and having it automagically converted to factors saying:

> Maybe when you do an uncommon operation like reading in a file, your numbers will be silently converted into factors / categorical variables. Or maybe not. Ha ha.

For all the advanced analysis packages in R you&#8217;d think that reading the data in would be important. Indeed, <a href="http://erehweb.wordpress.com/2009/05/26/r-and-data/#comment-31" target="_blank">commenter Nina</a> says it best:

> [data import in R] is like that joke about boats: the worst thing you can do with them is put them in the water. The worst thing you can do with R is give it data…

I have no doubt that there is some command that will prevent R from randomly converting a variable with 150 observations to a factor with 150 levels. However, after pouring through the help files and searching the web I have yet to find it. I will update with the answer if/when I find it.

via [R and data « Erehweb’s Blog][1].

**Update:** Turns out the problems were caused by CSV data saved by MS Excel. The numeric fields were stored as a number with comma separators so the number 1,000,000 was stored as &#8220;1,000,000&#8221; rather than &#8220;1000000&#8221;.  
Although I acknowledge that, in this case, R is not as much to blame as MS Excel for saving the comma to CSV or tab delimited files, I expect a quality analysis package to be smart enough to know that I&#8217;m not importing a factor series of 150 observations with 150 levels.

 [1]: http://erehweb.wordpress.com/2009/05/26/r-and-data/
---
title: 'Using -levelsof- to future-proof a loop through factorial variables in Stata'
author: Andrew
layout: post
permalink: /using-levelsof-to-future-proof-a-loop-through-factorial-variables-in-stata/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
categories:
  - Programming
tags:
  - data
  - Programming
  - Stata
---
Stata&#8217;s -[levelsof][1]- command was a solution to a problem I encountered the other day when I had to write a script that looped through a dataset and was one that I previously didn&#8217;t know about. In general, I feel that if you find yourself making looping through observations in a dataset or creating many nested loops, there is a good chance there&#8217;s a better way of tackling the problem at hand. That said, below I&#8217;ll outline how one might use -levelsof- that can help you future-proof your Stata scripts. Before you get started incorporating this in your do-file, read up on -[bysort][2]-, which I won&#8217;t get into here but could save you much coding and headache.

**You&#8217;ve just opened a large dataset with several factor variables**  
For now, I won&#8217;t ask why you want to loop through groups in a large dataset but assume that you&#8217;ve made up your mind to do so. Here is what you might like to do for a dataset with two factor variables, City and Gender, which are stored as strings:

<pre class="brush: perl; title: ; notranslate" title="">* sets up some locals with the levels of each factor variable
local genders "male female"
local cities "Vancouver Boston"

* a loop through the groups
foreach c of local cities {
    foreach g of local genders {
        quietly summarize hockey_spirit if gender == "`g'" & city == "`c'", meanonly
        local m = r(mean)
        di "Hockey spirit for `g' people in `c' is `m'"
    }
}
</pre>

**An alternative**  
The above example works fine in this case, but if there are many cities we might not want to type out all the options into a local and store it in the script. Furthermore, we might expect that the number of cities in our dataset will change at some point so we&#8217;d like to future-proof ourselves a little. 

Also, there may be some cities where only male or only female observations are present. Perhaps the gender data for some of the observations are collected with an [open text field][3], thus allowing the gender variable to have more than two options.

This is where -levelsof- can help you with looping across factor variables. Adapting the example above to the situation where we have 30 hockey cities and some of these cities have 3 or more reported genders, while others do not, we could use:

<pre class="brush: perl; title: ; notranslate" title="">* a loop through the groups
quietly levelsof city, local(cities)
foreach c of local cities {
    quietly levelsof gender if city == "`c'", local(genders)
    foreach g of local genders {
        quietly summarize hockey_spirit if gender == "`g'" & city == "`c'", meanonly
        local m = r(mean)
        di "Hockey spirit for `g' people in `c' is `m'"
    }
}
</pre>

Hope this is useful and happy coding!

 [1]: http://www.stata.com/help.cgi?levelsof
 [2]: http://www.stata.com/help.cgi?bysort
 [3]: http://smarterware.org/7388/the-case-against-drop-down-identities
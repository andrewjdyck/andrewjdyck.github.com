---
title: Collapsing multiple date variables in Stata
author: Andrew
layout: post
permalink: /collapsing-multiple-date-variables-in-stata/
categories:
  - Research
tags:
  - analysis
  - code
  - data management
  - panel data
  - Stata
---
I recently spoke with a friend who was working with a large dataset of information about head injury patients they are using in a research project. I&#8217;ve always said that for every day you expect to spend in data analysis, you can expect a week in data management just to prepare your dataset for analysis. This friend of mine has been finding just that and had a question about what to do when patients in his dataset have multiple dates of injury, recorded in multiple columns. The data he had was organized so that a patient has an entry in a date variable when the first arrive at the hospital and another entry in a second date variable if upon their next hospital visit.

Reformatting these multiple date variables into a single date variable for analysis is fairly straight-forward in Stata and utilizes the always handy egen command. What we&#8217;ll do is make use of the fact that Stata treats dates as numbers starting at 0 = January 1, 1960 then add the variables together and make sure Stata treats missing values as zero rather than missing. I&#8217;ll be using sample data for this example but you can get it from within Stata using the code below.

> use &#8220;http://andrewdyck.com/stata/PatientInjurySampleData.dta&#8221;, clear  
> egen AllDates = rowtotal(Date*)  
> format AllDates %d

Now you should have a new variable, AllDates, that you can use in some sort of panel data analysis. Have fun!
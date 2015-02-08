---
title: Regex, sql files, and panel data recoding on Statabytes
author: Andrew
layout: post
permalink: /regex-sql-files-and-panel-data-recoding-on-statabytes/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
categories:
  - Programming
  - Software
tags:
  - Stata
---
I&#8217;ve written three posts for my blog on Stata in the last month or so. One includes a [neat little trick to use regex commands][1] to shorten -if- statements after a command run either interactively or in an do-file. I like this trick because it can be particularly helpful when you are trying to find records in a large or messy (or both! -shudder-) dataset. 

Another post is a rundown on [getting data from a database dump saved in a .sql file into Stata][2]. I&#8217;m a big fan of using a relational database, such as MySQL or PostgreSQL, in conjunction with any analysis in Stata. I hope to have more about working with relational databases in Stata in the future.

Lastly, you may want to checkout a post on [recoding observations in a panel dataset][3]. It&#8217;s a simple trick I picked up from a discussion on LinkedIn, but helpful nonetheless.

Also, Stata 12 is out now. Unlike with Stata 11, I don&#8217;t feel like the improvements in this version will yield more than $500 of value for me so I&#8217;m thinking about skipping this upgrade. My only concern is about incompatibility with other Stata users, especially on [Statalist][4], in ways currently unknown to me. I guess we&#8217;ll see how it goes&#8230;..

 [1]: http://statabytes.andrewdyck.com/blog/a-regex-hack-to-simplify-subsetting-using-the-if-statement/
 [2]: http://statabytes.andrewdyck.com/blog/loading-a-sql-file-into-stata/
 [3]: http://statabytes.andrewdyck.com/blog/recoding-a-panel-dataset-with-time-periods/
 [4]: http://www.stata.com/statalist/
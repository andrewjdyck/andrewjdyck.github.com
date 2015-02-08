---
title: Connect to MySQL database using Stata
author: Andrew
layout: post
permalink: /connect-to-mysql-database-using-stata/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:1:{i:0;s:3:"976";}'
categories:
  - Programming
tags:
  - MySQL
  - ODBC
  - Stata
---
Today the Stata Corp. blog [outlined a new feature introduced to Stata 11.1][1] that allows one to connect to an ODBC database without setting up a DSN. This is a nice addition and simplifies the process of loading ODBC data for those one-off projects. 

The blog post explains how to connect to database running on Microsoft&#8217;s SQL server. Below I&#8217;ll describe the process using a database on the open-source MySQL platform.

**Step 0: Download/Install the MySQL ODBC Driver**  
If you haven&#8217;t done this already, you must install an ODBC driver to connect to MySQL servers. You can [download the latest version of the MySQL ODBC driver][2] and install it by following the prompts.

**Step 1: Load data from your MySQL database using Stata**  
The following example code will connect to a MySQL database (worldstats) running on my local machine (localhost) and extract a unique ID and name using a SQL statement (&#8216;sql&#8217;) from a table of country attributes (countries). This database requires a username (UID=andrew) and password (PWD=pass) but these may not be needed depending on how the server you are connecting to is configured.

<pre class="brush: perl; title: ; notranslate" title="">local db "DRIVER={MySQL ODBC 5.1 Driver};SERVER=localhost;DATABASE=worldstats;UID=andrew;PWD=pass;"
local sql "SELECT ID, CountryName FROM countries"

odbc load, exec("`sql'") conn("`db'") clear
des
</pre>

For more info about using -odbc- in Stata search the help files by typing &#8220;help odbc&#8221;. Good luck!

 [1]: http://blog.stata.com/2010/11/10/connection-string-support-added-to-odbc-command/
 [2]: http://dev.mysql.com/downloads/connector/odbc
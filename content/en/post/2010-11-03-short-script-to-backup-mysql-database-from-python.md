---
title: "Short script to backup MySQL database from Python"
author: Andrew
draft: false
date: 2010-11-03
# permalink: /short-script-to-backup-mysql-database-from-python/
tags: ["SQL", "MySQL", "Python"]
---

Although [MySQL][1] is normally thought of as the relational database management system that many websites are built on, I&#8217;ve found it to be pretty useful for many non-web tasks. Some advantages to using MySQL is that it&#8217;s cross platform so I can use it on my Linux and Windows computers and the availability of the gui tool [phpMyAdmin][2] which is also cross-platform. 

If you use phpMyAdmin, or you&#8217;re a linux geek, you know that backing up your MySQL database to a .sql file is easy. There is a point-and-click interface for phpMyAdmin and you can use mysqldump in a terminal on linux. Turns out this also works on windows with a small tweak and can be called from a Python script as well if you are using that language for development&#8230;.and if you&#8217;re not you should really consider it.

**Steps to backup a MySQL database running on windows from Python**

1. My default install of WAMP2 for Windows 7 didn&#8217;t set an environment variable for the MySQL folder so I added it by adding the text &#8220;;C:\wamp\bin\mysql\MySQL 5.1.36\bin&#8221; without quotes to the windows PATH by right clicking &#8220;My Computer&#8221; > Properties > Advanced settings > Environment variables.

2. Now you should be able to run mysql from the command line from any folder. Try it by opening a command window (win + r > cmd > OK) and typing: &#8220;mysql -u username&#8221;. Pretty cool.

3. Now you&#8217;re set to run MySQL commands from Python (or PHP, etc. as well I imagine). The following few lines of code will backup an entire database to a temporary directory in your root directory. Good luck!

<pre class="brush: python; title: ; notranslate" title="">import os
target_dir = 'C:\\TEMP\\'
os.system("mysqldump --add-drop-table -c -u username -ppassword database &gt; "+target_dir+"database.bak.sql")
</pre>

 [1]: http://www.mysql.com/
 [2]: http://www.phpmyadmin.net/
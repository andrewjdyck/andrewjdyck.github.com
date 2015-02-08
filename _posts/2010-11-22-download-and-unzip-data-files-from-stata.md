---
title: Download and unzip data files from Stata (Linux/Windows)
author: Andrew
layout: post
permalink: /download-and-unzip-data-files-from-stata/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:2:{i:0;s:3:"964";i:1;s:4:"2035";}'
categories:
  - Programming
tags:
  - linux
  - R
  - Stata
  - Windows
---
Recently, I&#8217;ve been using Stata&#8217;s -shp2dta- command to convert some shapefiles to stata format, grabbing Lat/Lon data and merging into another dataset. There were several compressed shapefiles I wanted to download contained in a directory from the web. I could manually download each file and uncompress each one but that would be time consuming. Also, when the maps are updated, I&#8217;d have to do the download/uncompress all over again. I&#8217;ve found that the process can be automated from within Stata by using a combination of -shell- and some handy terminal commands. If you are using Windows, you&#8217;ll need an additional set of command-line utilities called [Unix Utils][1].

Steps to download and start using compressed data are outlined below.

**step one (skip if Linux user): **

  1. [Download Unix Utilities for Windows][1]
  2. Unzip Unix tools to a directory of your choice. I put them in my &#8220;Program Files&#8221; directory.
  3. Browse through the directory you just created to find the folder where the executable files are. After extracting the files the executables were in: <pre class="brush: bash; title: ; notranslate" title="">C:\Program Files\usr\local\wbin\
</pre>

  4. Add this directory to your system PATH variable. You do this so that you can call these commands from the terminal from any folder on your hard drive. In my case I right clicked My Computer, selected properties > Advanced settings > Environment Variables, then edit the &#8220;path&#8221; variable adding the text &#8220;;C:\Program Files\usr\local\wbin\&#8221; without quotation marks. Be careful not to add a space between the semi-colon and the directory name.

**Step two:**

Open Stata and run the following commands or add them to a do-file.

Change to a working directory (e.g. cd &#8220;C:\Temp&#8221;)

Download the file to a file called download.zip by issuing the command:

<pre class="brush: perl; title: ; notranslate" title="">shell wget -Odownload.zip "http://example.com/download.zip"
</pre>

This command will use Stata&#8217;s -shell- command to send the text following to your operating system&#8217;s shell. For the command above this will use the unix utility wget to download a compressed file.

Now that the file is downloaded we need to unzip the compressed archive. On Windows I prefer to use 7zip for compression, but you could also use gzip from the Unix Utils package or unzip if you&#8217;re on Linux. I&#8217;ve included all three of these options below so choose one. Again, we submit the commands to Stata with the prefix -shell- so it sends the command to the OS shell.

<pre class="brush: perl; title: ; notranslate" title="">shell 7z x -o.\unZipped download.zip
shell gzip -d download.zip
shell unzip download.zip
</pre>

Including these in a do-file is extra useful as it automates the download and unzipping process. Be careful using wget in a do-file though, especially if you are trying to debug a your code. Some webmasters won&#8217;t like you downloading files multiple times and using up their bandwidth and this can get you blocked.

I haven&#8217;t tried it yet, but, I imagine that -shell- could be used to call other handy command line tools like Python scripts or maybe even leverage some useful R packages. I&#8217;ll post again if I have any luck with these options.

Now it&#8217;s time to dive into the data contained in those compressed archives and unlock their secrets. Good luck!!

 [1]: http://sourceforge.net/projects/unxutils/
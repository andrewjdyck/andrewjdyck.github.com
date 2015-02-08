---
title: Installing Stata on Ubuntu or Linux Mint
author: Andrew
layout: post
permalink: /installing-stata-on-ubuntu-or-linux-mint/
aktt_tweeted:
  - 1
aktt_notify_twitter:
  - yes
status_net:
  - yes
openid_comments:
  - 'a:3:{i:0;s:3:"487";i:1;s:3:"978";i:2;s:4:"1706";}'
categories:
  - Software
tags:
  - Stata
  - statistics
  - tutorial
---
For those like myself who have recently switched to the Linux operating system, installing programs that are not in the Ubuntu repositories can be a challenge at times. I recently installed the statistical analysis program Stata on my computer running the latest stable version of Linux Mint Gloria, which is a fork of the popular Ubuntu Linux distribution. But, more about my choice of Linux distro later. On to installing Stata on linux.

<pre class="brush: bash; title: ; notranslate" title="">sudo mkdir /usr/local/stata10
cd /usr/local/stata10
sh /media/cdrom/install
</pre>

Next, follow the prompts to install the program. The Stata install CD includes versions for several operating system so just pay attention. If you want to run the GUI version of Stata just like on windows then you&#8217;ll want to select the dynamically linked version in step three of the install.

After the files have been copied run the license install program by typing:

    sudo ./stinit

If there is an error you may need to change the permissions on the stata10 folder before starting the license program. Try typing:

<pre class="brush: bash; title: ; notranslate" title="">sudo chmod -R 755 /usr/local/stata10</pre>

Enter the serial number, code, and authorization key and you&#8217;ll be prompted to enter some info that will appear when Stata starts. I chose to enter my name on the first line and my job title on the second. Now you should be able to run Stata from the command line by typing:

<pre class="brush: bash; title: ; notranslate" title="">./stata</pre>

or you can run the GUI version of Stata by typing:

<pre class="brush: bash; title: ; notranslate" title="">./xstata</pre>

At first try I was able to run Stata from the command line but when I tried to run xstata I got the following error:

<pre class="brush: bash; title: ; notranslate" title="">./xstata: error while loading shared libraries: libtiff.so.3: cannot open shared object file: No such file or directory</pre>

After consulting a document on the Stata website, I was still confused about what to do but after further search I was able to run xstata by running the following commands. If you are running a recent version of Ubuntu such as 9.04 &#8211; 10.04 the following should work:

<pre class="brush: bash; title: ; notranslate" title="">sudo ln -s /usr/lib/libtiff.so.4 /usr/lib/libtiff.so.3</pre>

After upgrading to the latest version of Ubuntu, Maverick Meerkat (10.10), a new version of libtiff is included so the following softlink should be used instead of the line above.

<pre class="brush: bash; title: ; notranslate" title="">sudo ln -s /usr/lib/libtiff.so.4.3.3 /usr/lib/libtiff.so.3</pre>

Mostly, this post serves as a reminder to myself how to re-install if I have to but if you find this useful, leave me a comment below. Good luck!
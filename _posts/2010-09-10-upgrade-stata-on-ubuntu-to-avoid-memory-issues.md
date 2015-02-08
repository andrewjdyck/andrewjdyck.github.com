---
title: Upgrade Stata on Ubuntu to avoid memory issues
author: Andrew
layout: post
permalink: /upgrade-stata-on-ubuntu-to-avoid-memory-issues/
aktt_notify_twitter:
  - yes
status_net:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:1:{i:0;s:3:"483";}'
categories:
  - Programming
tags:
  - Stata
---
I use Stata 11 MP 64-bit on my computer at work which runs Windows 7. On this machine it runs spectacularly well, however, I have had some trouble running Stata on my laptop which runs on Ubuntu Linux (Lucid 10.04). Below is a description of the problem and the (very easy) solution.

**The problem**  
I noticed that when I ran my Stata scripts on Ubuntu, random characters would be added to the data (especially string data) when running the `reshape` command. For example, I would load some data:

`<br />
insheet using "/home/data/sample.csv", clear comma<br />
tabulate string_variable<br />
`

producing the output:

`<br />
string_vari |<br />
       able |      Freq.     Percent        Cum.<br />
------------+-----------------------------------<br />
          A |        500       50.00       50.00<br />
          B |        500       50.00      100.00<br />
------------+-----------------------------------<br />
      Total |      1,000      100.00<br />
`

Then I reshape the data in some manner and tabulate once more and find that `string_variable` has some new additions.

`<br />
string_vari |<br />
       able |      Freq.     Percent        Cum.<br />
------------+-----------------------------------<br />
          A |        498       49.80       49.80<br />
          B |        497       49.70       99.50<br />
       ôèA |           2        0.20        99.70<br />
      ñBúõ |           3        0.30      100.00<br />
------------+-----------------------------------<br />
      Total |      1,000      100.00<br />
`

Obviously it is a problem when random characters are being thrown into your data, especially if this is happening on a variable you use to index a `reshape` of the dataset. Now, on to how it&#8217;s fixed.

**The solution**  
I spent a great deal of time checking and re-checking my code because I believed that this must be something wrong with what I&#8217;m doing. After several hours of debugging and web searches the best I came up with is from [this thread on statalist][1] that suggested to me that maybe Stata thought that my license was invalid. I contacted Stata tech support to ask if there was a problem with my license and they told me this was NOT the case. Rather, a known bug with Ubuntu 10.04 due to the behavior of a low-level call in a library in this distribution of Linux caused data in Stata&#8217;s memory to become corrupted. Since it is a known bug, Stata issued a patch in Stata 11.1 and all that I needed to do is update the software. To do this first save your dataset and do-files if you&#8217;re working on something and then enter:

`<br />
update query<br />
update executable, force<br />
update swap<br />
`

When Stata restarts enter:

`<br />
update ado, force<br />
`

Now you should be on your way. If problems continue you&#8217;ll likely need to contact Stata tech support for more info but this fixed it for me.

 [1]: http://www.stata.com/statalist/archive/2008-12/msg00454.html
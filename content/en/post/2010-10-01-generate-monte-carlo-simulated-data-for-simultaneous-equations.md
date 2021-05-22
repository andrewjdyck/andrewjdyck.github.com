---
title: "Generate monte-carlo simulated data for simultaneous equations"
author: Andrew
date: 2010-10-01
draft: false
# permalink: /generate-monte-carlo-simulated-data-for-simultaneous-equations/
tags: ["Stata", "monte-carlo", "statistics"]
---

There are many sources around the net describing how to use two-stage least squares (2sls) to estimate a system of simultaneous equations. I won&#8217;t get into the nitty-gritty of simultaneous equations here because there is plenty out there on the web. My purpose for this post is to simply show how one can create an arbitrary dataset that one can use to test the assumptions of estimators used for simultaneity problems. Exploring a known data generating process is a great way to learn about how different estimators perform under different circumstances. In my example I will use a system with two dependent variables, Y1 and Y2, and one independent variable, X1. Note that since this system has only one exogenous variable (X1) it is under-identified.

The procedure goes like this:

  1. Write out the equations in your system
  2. Re-write the system as two equations expressed as functions of exogenous variables only
  3. Generate the variables in your software package of choice. I&#8217;ll be using Stata although this would be equally easy in R and in python you should be able to solve the systems and generate the data in the program and avoid the algebra.

1. Write out the system of equations:

Y1 = a0 + a1\*Y2 + a2\*X1 + e1  
Y2 = g0 + g1*Y1 + e2

where a0,a1,a2,g0 and g1 are parameters that we specify explicitly while e1 and e2 are error terms.

2. We can re-write the system of equations like this using simple substitution:

Y1 = (a0 + a1\*g0 + a1\*e2 + a2\*x1 + e1)/(1 &#8211; a1\*g1)  
Y2 = (g0 + g1\*a0 + g1\*a2\*x1 + g1\*e1 + e2)/(1 &#8211; g1*a1)

3. The following code will produce a dataset with simultaneously determined equations. Copy and paste into Stata and hit enter.

<pre class="brush: perl; title: ; notranslate" title="">clear
set obs 1000

* These are the random variables
gen x1 = rnormal(0,1)
gen e1 = rnormal(0,1)
gen e2 = rnormal(0,1)&lt;/code&gt;

* These are the parameters of our equations
* They can be any value you choose
local a0 = 1
local a1 = 2
local a2 = 3
local g0 = 4
local g1 = 5

* This generates our two dependent variables
gen y1 = (`a0' + `a1'*`g0' + `a1'*e2 + `a2'*x1 + e1)/(1-`a1'*`g1')
gen y2 = (`g0' + `g1'*`a0' + `g1'*`a2'*x1 + `g1'*e1 + e2)/(1-`g1'*`a1')
</pre>

Done! 

4. Now, since we know the data generating process (DGP) of this dataset, we should use it to test some of the assumptions of the 2SLS estimator. I&#8217;ll explore the 2SLS estimator in an upcoming post but to get you started you can try estimating the parameters using the -ivregress- command below.

<pre class="brush: perl; title: ; notranslate" title="">ivregress 2sls y2 (y1 = x1)
</pre>

Notice that the estimated coefficient on Y1 and intercept are 5.003 and 3.984 respectively. These are close to our input parameters so looks like the 2sls procedure works fairly well for this system. Now compare this to the results we&#8217;d find if we just used ordinary least squares (OLS).

<pre class="brush: perl; title: ; notranslate" title="">regress y2 y1
</pre>

This time we get an estimate for the coefficient on Y1 and intercept of 3.82 and 2.79 respectively. Not good, especially considering that Stata is reporting both of these estimates to be statistically significant.
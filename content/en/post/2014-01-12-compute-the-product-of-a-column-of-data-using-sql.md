---
title: "Compute the product of a column of data using SQL"
date: 2014-01-12
tags: ["SQL"]
draft: false
#permalink: /compute-the-product-of-a-column-of-data-using-sql/
#categories: ["Programming", "SQL"]
---

In SQL, summing a column of numbers is relatively trivial, and the size of the dataset isn&#8217;t important. For example:

<pre class="brush: sql; title: ; notranslate" title="">SELECT 
  SUM(X) as SUMOFX
FROM data_table;
</pre>

Mathematically, what we are doing here is:

$$SUMOFX = \sum\_{i=1}^n X\_i$$

Now, if we find ourselves in the unfortunate situation to compute this:

$$PRODUCTOFX = \prod\_{i=1}^n X\_i$$

In this case, it won&#8217;t be as easy to use the SQL code above, but we can use [Euler&#8217;s number][1] and a property of the [natural logarithm][2] to also make this task a trivial one. The equation that we are going to exploit is:

$$ln(x*y) = ln(x) + ln(y)$$

which gives us a functional relationship between the product and sum of two numbers. This allows us to change our above SQL code to:

<pre class="brush: sql; title: ; notranslate" title="">SELECT
  exp(sum(log(X))) as PRODUCTOFX
FROM data_table;
</pre>

It's probably really rare for this to be useful in any sort of production environment, however, I hope that this trick could save someone the hassle of having to code up a custom solution to compute a product for data that&#8217;s already in a relational database.

Good luck!

 [1]: http://en.wikipedia.org/wiki/E_(mathematical_constant)
 [2]: http://en.wikipedia.org/wiki/Natural_logarithm
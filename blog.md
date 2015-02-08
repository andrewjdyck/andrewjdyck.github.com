---
layout: page
title: Blog
---

{% for post in site.posts: 0 limit: 5 %}
<h4><strong><a href="{{ post.url }}">{{ post.title }}</a></strong></h4>
<p>
  {{ post.summary }}
</p>

{{ post.date | date: "%B %e, %Y" }}
<a href="{{ post.url }}">Read more</a>

{% endfor %}

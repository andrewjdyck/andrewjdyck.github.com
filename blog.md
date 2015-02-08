---
layout: page
title: Blog
---

<div class="content-section-a">
        <div class="container">
            <div class="row">
                <div class="col-lg-5 col-sm-6">
                    <hr class="section-heading-spacer">
                    <div class="clearfix"></div>
                    <h2 class="section-heading">{{ page.title }}</h2>

{% for post in site.posts: %}
{{ post.date | date: "%B %e, %Y" }}
<h4><strong><a href="{{ post.url }}">{{ post.title }}</a></strong></h4> 
<!--<p>
  {{ post.summary }}
</p>-->
<!--<a href="{{ post.url }}">Read more</a>-->

{% endfor %}


              </div>
            </div>

        </div>
        <!-- /.container -->

    </div>

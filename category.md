---
layout: page
title: Categories
permalink: /category/
---
{% for category in site.categories %}[{{ category | first }}](#{{ category | first }}) {% endfor %}

{% for category in site.categories %}
<h2><a name="{{ category | first }}">#{{ category | first }}</a></h2>

{% for post in category.last %}
<span class="pull-right">{{ post.date | date_to_long_string }}</span>[{{ post.title }}]({{ post.url }})

{% endfor %}

{% endfor %}
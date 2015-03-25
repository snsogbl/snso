---
layout: page
title: Tags
permalink: /tag/
---
{% for tag in site.tags %}[{{ tag | first }}](#{{ tag | first }}) {% endfor %}

{% for tag in site.tags %}
<h2><a name="{{ tag | first }}">#{{ tag | first }}</a></h2>

{% for post in tag.last %}
<span class="pull-right">{{ post.date | date_to_string }}</span>[{{ post.title }}]({{ post.url }})
{% endfor %}{% endfor %}

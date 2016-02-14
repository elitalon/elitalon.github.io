---
layout: page
title: Archive
---
{% for post in site.posts %}
  * {{ post.date | date_to_string }} &ndash; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
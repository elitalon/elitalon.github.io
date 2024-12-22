---
layout: page
title: Archive
---
{% assign postsByYear = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}

{% for year in postsByYear %}
## {{ year.name }}

<ul class="archive-list">
{% for post in year.items %}
<li class="archive-list-item">
  <span class="archive-list-item-date">{{ post.date | date: "%B %d" }}</span>
  <span class="archive-list-item-title" markdown="1">[{{ post.title }}]({{ post.url }})</span>
</li>
{% endfor %}
</ul>

{% endfor %}

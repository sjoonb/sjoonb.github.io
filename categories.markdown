---
layout: page
title: Categories
permalink: /cateogries/
---

<ul>
{% for category in site.categories %}
  <li><a name="{{ category | first }}" style="color: #000000; text-decoration: none;">{{ category | first }}</a>
    <ul>
    {% for post in category.last %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
    </ul>
    <br/>
  </li>
{% endfor %}
</ul>


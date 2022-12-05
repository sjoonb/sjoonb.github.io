---
# Feel free to add content and custom Front Matter to this file.
https://60devs.com/adding-comments-to-your-jekyll-blog.html
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

```
bundle exec jekyll serve --livereload
```

# Categories

<!-- <ul>
{% for category in site.categories %}
<details>
  <summary><a name="{{ category | first }}" style="color: #000000; text-decoration: none;">{{ category | first }}</a></summary>
    <ul>
    {% for post in category.last %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
    </ul>
</details>
{% endfor %}
</ul> -->


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



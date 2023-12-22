---
title: Posts
---
<div class="row">
{% for cat in site.categories %}
<div class="cat-col">
  <h3>{{ cat[0] }}</h3>
  <ul>
    {% for post in cat[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  </div>
{% endfor %}
</div>
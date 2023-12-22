---
title: Recipes
---
<div class="row">
{% assign myrecipes = site.recipes | group_by: 'category' %}
{% for cat in myrecipes %}
<div class="cat-col">
  <h2>{{ cat.name | capitalize }}</h2>
  <ul>
    {% assign items = cat.items | sort: 'title' %}
    {% for item in items %}
      <li><a href="{{ item.url }}">{{ item.title }}</a></li>
    {% endfor %}
  </ul>
  </div>
{% endfor %}
</div>


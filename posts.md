---
title: Posts
---
<div class="row">
{% for cat in site.categories %}
  <div class="cat-col">
    <h3>{{ cat[0] }}</h3>
    {% assign posts_by_month = cat[1] | group_by_exp: "post", "post.date | date: '%B %Y'" %}
    {% for month in posts_by_month %}
      <h4>{{ month.name }}</h4>
      <ul>
        {% for post in month.items %}
          <li><a href="{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
      </ul>
    {% endfor %}
  </div>
{% endfor %}
</div>
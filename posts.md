---
title: Posts
---

<div class="row">
  <div class="cat-col">
    {% assign posts_by_month = site.posts | group_by_exp: "post", "post.date | date: '%B %Y'" %}
    {% for month in posts_by_month %}
      <h3>{{ month.name }}</h3>
      <ul>
        {% for post in month.items %}
          <li><a href="{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
      </ul>
    {% endfor %}
  </div>
</div>

---
title: Tech Notes
---
{% assign mynotes = site.tech_notes | group_by: 'topic' %}
{% for cat in mynotes %}
  <h3>{{ cat.name | capitalize }}</h3>
  <ul>
    {% assign items = cat.items | sort: 'title' %}
    {% for item in items %}
      <li><a href="{{ item.url }}">{{ item.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
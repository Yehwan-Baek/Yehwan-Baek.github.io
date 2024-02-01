---
layout: category
title: Projects in Academy Xi
---

{% for post in site.categories.projects-in-academy-xi %}
  <li><a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}

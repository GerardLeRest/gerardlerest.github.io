---
layout: default
title: "Catégories"
permalink: /categories/
---

<h1>Catégories</h1>

<ul>
  {% assign categories = site.categories | sort %}
  {% for category in categories %}
    <li>
      <a href="/categories/{{ category[0] | slugify }}/">
        {{ category[0] }} ({{ category[1].size }})
      </a>
    </li>
  {% endfor %}
</ul>


---
layout: page
title: Archives
---

Here is a full list of all the posts on this site.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

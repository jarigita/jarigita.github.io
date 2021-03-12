---
title:  "Blogs"
layout: archive
permalink: /Blogs/
author_profile: true
comments: true
---

Most of my blogs are technical blogs written mainly for my own reference. I'd be happy if any of you find them useful too.



<ul>
  {% for post in site.posts %}
    <img src="/{{post.header.image}}" alt="{{post.title}}">
    {% include archive-single.html %}
  {% endfor %}
</ul>

## Notebooks:
- [**Python: assignment, function argument passing, views, and copies**](https://github.com/zengliX/Notebooks/blob/master/python_variable.ipynb)


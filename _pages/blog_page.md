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
    <figure>
      <a href="{{post.url}}"><img src="/{{post.header.overlay_image}}" alt="{{post.title}}"></a>
    </figure>
    {% include archive-single.html %}
  {% endfor %}
</ul>

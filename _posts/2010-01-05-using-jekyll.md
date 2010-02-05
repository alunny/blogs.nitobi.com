---
layout: post
title: Using Jekyll For My Blog
category: jekyll
---

This is my first post using Jeykll!
{% for category in site.categories %}
  {{ category }}
{% endfor %}
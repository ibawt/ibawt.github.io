---
layout: default
title: index
---
# Latest Article:
{% for post in site.posts limit:1 %}
{% include post_snippet.html param=post %}
{% endfor %}
There's not much here yet.  Checkout my batman.js tutorials above.


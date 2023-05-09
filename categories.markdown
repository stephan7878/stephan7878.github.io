---
layout: page
title: Categories
permalink: /categories/
---


{% for category in site.categories %}

{% capture category_name %}{{ category | first }}{% endcapture %}

## {{ category_name | capitalize }}

{% for post in site.categories[category_name] %}

- [{{post.title}}]({{ site.baseurl }}{{ post.url }})

{% endfor %}

{% endfor %}

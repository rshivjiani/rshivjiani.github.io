---
title: Archives
layout: page
permalink: /archives
---

{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
   <h4 id="y{{post.date | date: "%Y"}}">{{ currentdate }}</h4>
   <ul>
    {% assign date = currentdate %}
  {% endif %}
   <li>{{ post.date | date: "%b %Y" }} – <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}
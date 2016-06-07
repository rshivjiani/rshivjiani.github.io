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
   <li>{{ post.date | date: "%d %b %Y" }} – <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}

---

{% comment%}
=================
Here we generate all the categories.
=================
{% endcomment%}

{% assign rawcats = "" %}
{% for post in site.posts %}
    {% assign tcats = post.category | join:'|' | append:'|' %}
    {% assign rawcats = rawcats | append:tcats %}
{% endfor %}

{% assign rawcats = rawcats | split:'|' | sort %}
{% assign cats = "" %}

{% for cat in rawcats %}
    {% if cat != "" %}
        {% if cats == "" %}
            {% assign cats = cat | split:'|' %}
        {% endif %}

        {% unless cats contains cat %}
            {% assign cats = cats | join:'|' | append:'|' | append:cat | split:'|' %}
        {% endunless %}
    {% endif %}
{% endfor %}


#### Categories

<ul>
{% for ct in cats %}
<li><a href="#{{ ct | slugify }}">{{ ct }}</a></li>
{% endfor %}
<li><a href="#no-category">No category</a></li>
</ul>

{% for ct in cats %}
<h4 id="{{ ct | slugify }}">{{ ct }}</h4>
<ul>
    {% for post in site.posts %}
        {% if post.category contains ct %}
        <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <small>{{ post.date | date_to_string }}</small>
        </li>
        {% endif %}
    {% endfor %}
</ul>
{% endfor %}

<h4 id="no-category">No category</h4>
<ul>
    {% for post in site.posts %}
        {% unless post.category %}
            <li>
            <a href="{{ post.url }}">{{ post.title }}</a>
            <small>{{ post.date | date_to_string }}</small>
            </li>
        {% endunless %}
    {% endfor %}
</ul>
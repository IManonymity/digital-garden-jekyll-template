---
title: Home
permalink: /
---

# Welcome! 🌱

<ul>
{% for note in site.notes %} 
<li> 
<h2><a href="{{ note.url }}">{{ note.title }}</a></h2> 
<h3>{{ note.tags }}</h3>
</li>
{% endfor %}
<ul>

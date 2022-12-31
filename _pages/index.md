---
title: Home
permalink: /
---

# Welcome! 🌱

<ul>
{% for note in site.notes %} 
<li> 
<h4><a href="{{ note.url }}">[{{ note.tags }}系列]{{ note.title }}</a></h4> 
</li>
{% endfor %}
<ul>

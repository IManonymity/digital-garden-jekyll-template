---
title: Home
permalink: /
date created: 星期五, 十二月 30日 2022, 7:17:09 晚上
date modified: 星期六, 十二月 31日 2022, 5:30:55 下午
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

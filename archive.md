---
layout: default
title: Archive
---

# archive

<ul>
{% for post in site.posts%}
<li>
<span>{{- post.date | date: "%Y-%m-%d"-}}: </span>
<a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>

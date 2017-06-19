---
layout: page
title: Wiki
description: 随便写写吧
keywords: 维基, Wiki
comments: false
menu: 维基
permalink: /wiki/
---

> 总是要记录一些东西的

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>

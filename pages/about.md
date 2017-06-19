---
layout: page
title: 我是谁
description: 摸爬滚些许年,代码行业小菜鸟
keywords: Cheney Chen,陈晨
comments: true
menu: 关于
permalink: /about/
---

我是陈晨，爱代码，爱生活。


坚信熟能生巧，努力改变人生。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

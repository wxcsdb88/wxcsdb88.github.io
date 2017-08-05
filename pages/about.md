---
layout: page
title: About
description: futurever coding
keywords: wxcsdb88, XIN WANG
comments: true
menu: 关于
permalink: /about/
---

Don’t waste time on trying to find meaning and purpose in life other than your instincts.

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

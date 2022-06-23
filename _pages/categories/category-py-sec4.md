---
title: "이분탐색(결정알고리즘) & 그리디 알고리즘"
layout: archive
permalink: categories/sec4
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.Sec4 %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}

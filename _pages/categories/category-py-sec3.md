---
title: "탐색 & 시뮬레이션 (string,1차원,2차원 리스트 탐색)"
layout: archive
permalink: categories/sec3
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.Sec3 %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}

---
layout: default
title: "Blog"
description: 관심 분야의 글을 작성합니다.
main: true
project-header: true
# header-img: img/about.jpg
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.blog == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>
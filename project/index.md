---
layout: default
work: true
main: true
title: Worked Projects
description: 지금까지 작업한 프로젝트입니다.
project-header: true
---

<div class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.projects == true %}

     {% include post-list.html %}

{% endif %}
{% endfor %}
</div>
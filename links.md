---
layout: page
title: 友链
permalink: links.html
image: /public/images/links.jpeg
order: 4
---

> 待取霜风送月来~

<ul class="links">
{% for item in site.links %}
<li>
    <p>
        <a href="{{ item.url }}" target="_blank" title="{{ site.title }}">
        {{ item.title }}
        </a>
    </p>
</li>
{% endfor %}
</ul>

---
title: "About"
layout: default
sitemap: false
permalink: /about/
---

<nav class="main-nav">
    <a class="back-button" href="{{ site.url }}">
        <i class="fa fa-th" aria-hidden="true"></i>
    </a>
    <a class="subscribe-button" href="{{ site.url }}/feed.xml">
        <i class="fa fa-rss" aria-hidden="true"></i>
    </a>
</nav>

{% if site.author %}
    {% assign author = site.data.authors[site.author] %}
    {{ author.bio }}
    "I haven’t been everywhere, but it’s on my list." – Susan Sontag
{% endif %}

{% include map.html %}

---
layout: default
title: "Home"
description: "Projects by Sunbochen Tang"
---

# Projects

<ul>
  {% assign sorted = site.projects | sort: 'year' | reverse %}
  {% for p in sorted %}
    <li>
      <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
      — {{ p.venue }}{% if p.year %} ({{ p.year }}){% endif %}
    </li>
  {% endfor %}
</ul>

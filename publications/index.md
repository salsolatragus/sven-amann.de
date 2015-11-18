---
title: Publications
menu_index: 4
author: Sven
layout: article
year: 3000
---

<dl>
{% for publication in site.data.publications %}
  {% if year != publication.year %}
    {% assign year = publication.year %}
    <dt><h2>{{ year }}</h2></dt>
  {% endif %}
  <dd>
    <a href="{{ publication.link }}"><em>{{ publication.title }}</em></a><br/>
	{{ publication.authors }}<br/>
	{{ publication.published_in }}
  </dd>
{% endfor %}
</dl>
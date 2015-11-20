---
title: Publications
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
    <p>
      <a href="{{ publication.link }}">{{ publication.title }}</a><br/>
	    {{ publication.authors }}<br/>
	    {{ publication.published_in }}
    </p>
  </dd>
{% endfor %}
</dl>
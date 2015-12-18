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
      <strong>
      {% if publication.link != nil %}
        <a href="{{ publication.link }}">
      {% endif %}
      {{ publication.title }}
      {% if !publication.link != nil %}
        </a>
      {% else %}
        <em>(Accepted)</em>
      {% endif %}
      </strong>
      <br/>
	    {{ publication.authors }}<br/>
	    {{ publication.published_in }}
    </p>
  </dd>
{% endfor %}
</dl>
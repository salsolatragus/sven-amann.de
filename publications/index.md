---
title: Publications
author: Sven
layout: article
year: 3000
---

<dl>
{% assign publications = site.publications | sort: "year" | reverse %}
{% for publication in publications %}
  {% if year != publication.year %}
    {% assign year = publication.year %}
    <dt><h2>{{ year }}</h2></dt>
  {% endif %}
  <dd>
    <p>
      <strong>
        <a name="{{ publication.key }}"></a><a name="{{ publication.slug }}"></a>
        <a href="{{ publication.url }}">{{ publication.title }}</a>
      </strong>
      <br/>
	    by {% for author_id in publication.authors %}
        {% if forloop.last %}{% unless forloop.first %}
          and
        {% endunless %}{% endif %}
        {% assign author = site.data.publication_authors[author_id] %}
        {% if author.mail %}<a href="mailto:{{ author.mail }}">{% endif %}{{ author.firstname }} {{ author.name }}{% if author.mail %}</a>{% endif %}{% unless forloop.last %},{% endunless %}
      {% endfor %}<br/>
      {% if publication.doi %}In{% elsif publication.publisher_link %}{% else %}To be published in{% endif %}
	    <em>{{ publication.published_in }}</em><br/>
      {% if publication.doi %}
        [<a href="http://dx.doi.org/{{ publication.doi }}">publication (via DOI)</a>]
      {% endif %}
      {% if publication.publisher_link %}
        [<a href="{{ publication.publisher_link }}">publication</a>]
      {% endif %}
      {% if publication.preprint != nul %}
        [<a href="{{ site.url }}/publications/{{ publication.preprint }}">preprint</a>]
      {% endif %}
      {% if publication.artifact_page != nul %}
        [<a href="{{ publication.artifact_page }}">artifact page</a>]
      {% endif %}
      {% if publication.slides %}
        [<a href="{{ publication.slides }}">slides</a>]
      {% endif %}
      {% if publication.images %}
        [<a href="{{ publication.images }}">slide images</a>]
      {% endif %}
    </p>
  </dd>
{% endfor %}
</dl>
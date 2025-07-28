---
layout: default
title: FDA-NIH Modernizing Research and Evidence (MoRE) Glossary
---

{% comment %}
  1. Get all mds from the 'terms' collection and sort them alphnumerically by the 'term' variable.
{% endcomment %}
{% assign sorted_terms = site.terms | sort: "term" %}

{% comment %}
  2. Group the sorted terms by the first letter of their 'term' variable.
     This creates groups like {"name": "A", "items": [...]}, {"name": "B", "items": [...]}, etc.
{% endcomment %}
{% assign grouped_terms = sorted_terms | group_by_exp: "item", "item.term | slice: 0, 1 | upcase" %}

<div class="container" id="top">
  <header>
    <h1>{{ page.title }}</h1>
    <p>Concensus definitions for use in clinical research and evidence.</p>
  </header>

  <nav class="alpha-nav">
    {% for group in grouped_terms %}
      <a href="#{{ group.name }}">{{ group.name }}</a>
    {% endfor %}
  </nav>

  <main>
    {% for group in grouped_terms %}
    <section id="{{ group.name }}" class="glossary-section">
      <h2>{{ group.name }}</h2>
      <dl>
        {% for item in group.items %}
          <dt>{{ item.term }}</dt>
          <dd>{{ item.definition | markdownify }}</dd>
        {% endfor %}
      </dl>
    </section>
    {% unless forloop.last %}<hr>{% endunless %}
    {% endfor %}
  </main>

  <footer>
    <a href="#top" class="back-to-top">↑ Back to Top</a>
  </footer>
</div>

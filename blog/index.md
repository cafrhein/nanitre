---
layout: default
title: Cuaderno
description: Procesos, notas y reflexiones desde el estudio de Daniela Trejo.
---

<section class="journal">
  <p class="eyebrow">Cuaderno de estudio</p>
  <h1 class="display">Procesos,<br>hallazgos y<br><em>reflexiones.</em></h1>
  <p class="section-intro">Notas sobre pintura, materia y el trabajo cotidiano detrás de cada pieza.</p>

  <div class="journal-list">
    {% for post in site.posts %}
    <article class="journal-item">
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%d · %m · %Y" }}</time>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <a href="{{ post.url | relative_url }}" aria-label="Leer {{ post.title }}">↗</a>
    </article>
    {% endfor %}
  </div>
</section>
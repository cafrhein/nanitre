---
layout: default
title: Obra
description: Portafolio de obra seleccionada de Daniela Trejo.
---

<header class="page-head">
  <div>
    <p class="eyebrow">Archivo / Obra seleccionada</p>
    <h1 class="display">Materia,<br>memoria y <em>afecto.</em></h1>
  </div>
  <p class="section-intro">Una selección de pinturas que observan aquello que permanece: los vínculos, los objetos y la forma en que la luz transforma la experiencia.</p>
</header>

<section class="portfolio-grid" aria-label="Portafolio de Daniela Trejo">
  {% for obra in site.portfolio %}
  <article class="portfolio-card">
    <a href="{{ obra.url | relative_url }}">
      <img src="{{ '/assets/img/' | append: obra.imagen_principal | relative_url }}" alt="{{ obra.title }}" loading="{% if forloop.index > 2 %}lazy{% else %}eager{% endif %}">
      <div class="portfolio-card__meta">
        <div>
          <h2>{{ obra.title }}</h2>
          <p>{{ obra.tecnica }} · {{ obra.dimensiones }} · {{ obra.anio }}</p>
        </div>
        <span class="portfolio-card__arrow" aria-hidden="true">↗</span>
      </div>
    </a>
  </article>
  {% endfor %}
</section>
---
layout: default
title: Inicio
description: Daniela Trejo, artista visual. Pintura, memoria y obra certificada.
---

<section class="home-hero">
  <div class="home-hero__copy">
    <p class="eyebrow">Daniela Trejo · Artista visual</p>
    <h1 class="display">Pintar es<br>conservar una <em>huella.</em></h1>
    <p class="home-hero__intro">Una práctica construida entre la materia, la memoria y la experiencia sensible.</p>
    <a class="text-link" href="{{ '/portfolio/' | relative_url }}">Explorar la obra <span aria-hidden="true">↗</span></a>
  </div>
  <figure class="home-hero__image">
    <img src="{{ '/assets/img/Mi-Lugar-Seguro.png' | relative_url }}" alt="Mi Lugar Seguro, obra de Daniela Trejo" fetchpriority="high">
  </figure>
</section>

<section class="manifesto">
  <p class="eyebrow">Práctica / 2018—presente</p>
  <blockquote>Trabajo con la pintura como un espacio de memoria y observación: un lugar donde los vínculos, los objetos y la luz dejan una <em>huella sensible.</em></blockquote>
</section>

<section class="featured" aria-labelledby="featured-title">
  <div class="featured__head">
    <div>
      <p class="eyebrow">Obra seleccionada</p>
      <h2 class="section-title" id="featured-title">Cuatro formas<br>de permanecer.</h2>
    </div>
    <p class="section-intro">Piezas que exploran el afecto, la espera, la belleza transitoria y la memoria contenida en los objetos.</p>
  </div>

  <div class="art-grid">
    {% assign featured_works = site.portfolio | slice: 0, 3 %}
    {% for obra in featured_works %}
    <article class="art-card">
      <a href="{{ obra.url | relative_url }}" aria-label="Ver {{ obra.title }}">
        <div class="art-card__image">
          <img src="{{ '/assets/img/' | append: obra.imagen_principal | relative_url }}" alt="{{ obra.title }}" loading="lazy">
        </div>
        <div class="art-card__meta">
          <span class="art-card__index">0{{ forloop.index }}</span>
          <h3>{{ obra.title }}</h3>
          <p>{{ obra.tecnica }} · {{ obra.anio }}</p>
        </div>
      </a>
    </article>
    {% endfor %}
  </div>
</section>

<section class="home-artist">
  <div class="home-artist__portrait">
    <img src="{{ '/assets/img/Daniela_Trejo.png' | relative_url }}" alt="Daniela Trejo, artista visual" loading="lazy">
  </div>
  <div class="home-artist__copy">
    <p class="eyebrow">La artista</p>
    <h2 class="section-title">Daniela<br>Trejo</h2>
    <p class="section-intro">Licenciada en Artes Visuales. Su práctica integra exploración creativa, oficio y una gestión rigurosa de cada proyecto, desde la primera intuición hasta la pieza certificada.</p>
    <a class="text-link" href="{{ '/perfil/' | relative_url }}">Conocer su trayectoria <span aria-hidden="true">↗</span></a>
  </div>
</section>

<section class="verify-callout">
  <div>
    <p class="eyebrow">Registro Nanitre</p>
    <h2 class="section-title">Cada obra tiene<br>una <em>historia verificable.</em></h2>
  </div>
  <div>
    <p>Consulta el identificador único de una pieza y confirma su registro, año y estado dentro del archivo público del estudio.</p>
    <a class="text-link" href="{{ '/verificacion/' | relative_url }}">Verificar certificado <span aria-hidden="true">↗</span></a>
  </div>
</section>
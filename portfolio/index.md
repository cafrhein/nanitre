---
layout: default
title: Portfolio
---

<header style="margin-bottom: 4rem;">
    <h1 style="font-size: 2.5rem; font-weight: 300; letter-spacing: -1px;">Portfolio</h1>
    <p style="color: var(--secondary-color);">Una selección de obras que exploran la materia, la forma y la experiencia digital.</p>
</header>

<section class="grid-layout">
    {% for obra in site.portfolio %}
    <article class="obra-card">
        <a href="{{ obra.url | relative_url }}">
            <img src="{{ site.baseurl }}/assets/img/{{ obra.imagen_principal }}" alt="{{ obra.title }}" class="img-fluid" style="filter: grayscale(100%); transition: filter 0.5s;" onmouseover="this.style.filter='grayscale(0%)'" onmouseout="this.style.filter='grayscale(100%)'">
        </a>
        <h3 style="font-size: 1.1rem; margin-top: 1.5rem; font-weight: 600; line-height: 1.2;">
            <a href="{{ obra.url | relative_url }}" style="text-decoration: none; color: inherit;">
                {{ obra.title }}
            </a>
        </h3>
        <p style="margin: 0.5rem 0 0 0; color: var(--secondary-color); font-size: 0.85rem; text-transform: uppercase; letter-spacing: 0.05em;">
            {{ obra.tecnica }} | {{ obra.anio }}
        </p>
    </article>
    {% endfor %}
</section>

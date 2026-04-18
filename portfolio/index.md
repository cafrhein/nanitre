---
layout: default
title: Portfolio
---

<header style="margin-bottom: 4rem;">
    <h1 style="font-size: 2.5rem; font-weight: 300; letter-spacing: -1px;">Obra</h1>
    <p style="color: var(--secondary-color);">Exploración de la plástica y diseño de experiencias.</p>
</header>

<section class="portfolio-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem;">
    {% for obra in site.portfolio %}
    <div class="obra-card">
        <a href="{{ obra.url | relative_url }}">
            <img src="{{ site.baseurl }}/assets/img/{{ obra.imagen_principal }}" alt="{{ obra.title }}" class="img-fluid" style="filter: grayscale(100%); transition: filter 0.5s;" onmouseover="this.style.filter='grayscale(0%)'" onmouseout="this.style.filter='grayscale(100%)'">
        </a>
        <h3 style="font-size: 1rem; margin-top: 1rem;">{{ obra.title }}</h3>
        <p style="font-size: 0.8rem; color: #888;">{{ obra.tecnica }} | {{ obra.anio }}</p>
    </div>
    {% endfor %}
</section>

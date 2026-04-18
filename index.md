---
layout: default
title: Inicio
---

<section style="padding: 4rem 0; text-align: center;">
    <h2 style="font-size: 3rem; font-weight: 300; margin-bottom: 1rem;">Nanitre</h2>
    <p style="color: var(--secondary-color); max-width: 600px; margin: 0 auto 2rem;">
        Bienvenido al espacio creativo de Edna Daniela Trejo Martínez. 
        Donde el arte contemporáneo convergen con el diseño de experiencias digitales.
    </p>
    <a href="{{ site.baseurl }}/portfolio" style="padding: 1rem 2rem; border: 1px solid var(--primary-color); text-decoration: none; color: var(--primary-color); font-size: 0.9rem; transition: all 0.3s;" onmouseover="this.style.backgroundColor='var(--primary-color)'; this.style.color='white'" onmouseout="this.style.backgroundColor='transparent'; this.style.color='var(--primary-color)'">
        Ver Portafolio
    </a>
</section>

<hr style="border: 0; border-top: 1px solid #f0f0f0; margin: 2rem 0;">

<div class="featured-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem;">
    {% for obra in site.portfolio limit:3 %}
    <div class="obra-card">
        <a href="{{ obra.url }}">
            <img src="{{ site.baseurl }}/assets/img/{{ obra.imagen_principal }}" alt="{{ obra.title }}" class="img-fluid" style="filter: grayscale(100%); transition: filter 0.5s;" onmouseover="this.style.filter='grayscale(0%)'" onmouseout="this.style.filter='grayscale(100%)'">
        </a>
        <h3 style="font-size: 1rem; margin-top: 1rem;">{{ obra.title }}</h3>
        <p style="font-size: 0.8rem; color: #888;">{{ obra.tecnica }} | {{ obra.anio }}</p>
    </div>
    {% endfor %}
</div>

---
layout: page
title: Perfil Artístico
permalink: /perfil/
---

<style>
  .profile-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 20px 60px 20px;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    line-height: 1.8;
    color: #222;
  }

  /* Contenedor de Portada (Full Width dentro del container) */
  .hero-container {
    width: 100%;
    margin: 20px 0 40px 0;
    overflow: hidden;
    border-radius: 2px;
    background: #f9f9f9;
  }

  .hero-image {
    width: 100%;
    height: auto;
    display: block;
    object-fit: cover;
    max-height: 450px; /* Altura máxima para no desplazar todo el texto */
  }

  /* Foto de Perfil Circular/Cuadrada refinada */
  .artist-photo {
    width: 160px;
    height: 160px;
    object-fit: cover;
    display: block;
    margin: -80px auto 20px auto; /* Efecto overlap sobre la portada */
    border: 4px solid #fff;
    border-radius: 50%; /* Foto circular para contraste con la portada rectangular */
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    position: relative;
    z-index: 2;
  }

  .artist-name {
    text-align: center;
    font-size: 2.4rem;
    font-weight: 300;
    letter-spacing: 2px;
    margin-bottom: 5px;
    text-transform: uppercase;
  }

  .artist-tagline {
    text-align: center;
    color: #777;
    margin-bottom: 50px;
    text-transform: uppercase;
    font-size: 0.85rem;
    letter-spacing: 3px;
  }

  .profile-content {
    max-width: 700px;
    margin: 0 auto;
  }

  .section-title {
    border-bottom: 1px solid #eee;
    display: block;
    margin: 40px 0 20px 0;
    padding-bottom: 10px;
    text-transform: uppercase;
    font-size: 0.9rem;
    letter-spacing: 2px;
    color: #444;
  }

  ul {
    padding-left: 20px;
    list-style-type: square;
  }

  li {
    margin-bottom: 10px;
  }

  /* Responsivo */
  @media (max-width: 768px) {
    .artist-name { font-size: 1.8rem; }
    .hero-image { max-height: 250px; }
    .artist-photo { width: 120px; height: 120px; margin-top: -60px; }
  }
</style>

<div class="hero-container">
  <img src="{{ '/assets/img/Daniela-Trejo-Portada-Web.png' | relative_url }}" 
       alt="Edna Daniela Trejo Martínez - Portada" 
       class="hero-image">
</div>

<div class="profile-container">
  
  <img src="{{ '/assets/img/Daniela_Trejo.png' | relative_url }}" 
       alt="Daniela Trejo" 
       class="artist-photo">

  <h1 class="artist-name">Daniela Trejo</h1>
  <p class="artist-tagline">Licenciada en Artes Visuales</p>

  <div class="profile-content">
    <p>
      Mi práctica artística integra la exploración creativa con un dominio riguroso de la técnica y la ejecución de proyectos de principio a fin.
    </p>

    <h3 class="section-title">Formación Académica</h3>
    <ul>
      <li><strong>Licenciatura en Artes Visuales</strong> – Escuela Nacional de Artes Plásticas (Generación 2009).</li>
      <li><strong>Taller: Dibujo de la figura humana</strong> – Antigua Academia de San Carlos (2019).</li>
    </ul>

    <h3 class="section-title">Gestión de Estudio</h3>
    <p>
      Desde 2018, me desempeño como <strong>Artista Visual y Gestora de Proyectos</strong>, 
      encargándome de la administración integral de marca, negociación directa con coleccionistas 
      y presupuestación de obra bajo estándares de alta calidad.
    </p>
  </div>

</div>

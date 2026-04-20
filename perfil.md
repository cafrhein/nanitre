---
layout: page
title: Perfil Artístico
permalink: /perfil/
---

<style>
  /* 1. Menú Superior Habilitado */
  /* Se han eliminado las reglas que ocultaban el header para mantener consistencia UX */

  /* Reset y Base para Full Width */
  .main-content {
    padding: 0 !important;
    max-width: 100% !important;
  }

  /* Portada Full Width */
  .hero-full-width {
    width: 100vw;
    position: relative;
    left: 50%;
    right: 50%;
    margin-left: -50vw;
    margin-right: -50vw;
    height: 45vh;
    min-height: 300px;
    background: #1a1a1a;
    overflow: hidden;
  }

  .hero-full-width img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  /* Contenedor de Contenido */
  .profile-wrapper {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 20px 60px 20px;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    line-height: 1.8;
    color: #222;
  }

  /* Foto de Perfil Circular Solapada */
  .artist-avatar {
    width: 180px;
    height: 180px;
    object-fit: cover;
    object-position: center 10%;
    display: block;
    margin: -90px auto 30px auto;
    border: 6px solid #fff;
    border-radius: 50%;
    box-shadow: 0 10px 25px rgba(0,0,0,0.15);
    position: relative;
    z-index: 10;
    background: #fff;
  }

  .artist-name {
    text-align: center;
    font-size: 2.6rem;
    font-weight: 300;
    letter-spacing: 3px;
    margin-bottom: 5px;
    text-transform: uppercase;
    color: #111;
  }

  .artist-tagline {
    text-align: center;
    color: #888;
    margin-bottom: 60px;
    text-transform: uppercase;
    font-size: 0.9rem;
    letter-spacing: 4px;
  }

  .profile-text-content {
    max-width: 700px;
    margin: 0 auto;
  }

  .section-divider {
    border-bottom: 1px solid #eaeaea;
    display: block;
    margin: 50px 0 25px 0;
    padding-bottom: 10px;
    text-transform: uppercase;
    font-size: 0.85rem;
    letter-spacing: 2px;
    color: #555;
    font-weight: bold;
  }

  /* Estilo del Botón Volver */
  .back-container {
    text-align: center;
    margin-top: 80px;
    padding-bottom: 40px;
  }

  .btn-back {
    display: inline-block;
    padding: 12px 35px;
    border: 1px solid #111;
    color: #111;
    text-decoration: none;
    text-transform: uppercase;
    font-size: 0.75rem;
    letter-spacing: 3px;
    transition: all 0.3s ease;
    cursor: pointer;
    background: transparent;
  }

  .btn-back:hover {
    background: #111;
    color: #fff;
  }

  /* Responsivo */
  @media (max-width: 768px) {
    .hero-full-width { height: 30vh; }
    .artist-name { font-size: 1.8rem; }
    .artist-avatar { 
      width: 140px; 
      height: 140px; 
      margin-top: -70px; 
    }
  }
</style>

<div class="hero-full-width">
  <img src="{{ '/assets/img/Imagen-Portada.png' | relative_url }}" 
       alt="Edna Daniela Trejo Martínez - Portada Artística">
</div>

<div class="profile-wrapper">
  
  <img src="{{ '/assets/img/Daniela_Trejo.png' | relative_url }}" 
       alt="Daniela Trejo" 
       class="artist-avatar">

  <h1 class="artist-name">Daniela Trejo</h1>
  <p class="artist-tagline">Licenciada en Artes Visuales</p>

  <div class="profile-text-content">
    <p>
      Mi práctica artística integra la exploración creativa con un dominio riguroso de la técnica y la ejecución de proyectos de principio a fin, enfocada en la intersección entre lo analógico y lo digital.
    </p>

    <h3 class="section-divider">Formación Académica</h3>
    <ul>
      <li><strong>Licenciatura en Artes Visuales</strong> – Escuela Nacional de Artes Plásticas (Generación 2009).</li>
      <li><strong>Taller: Dibujo de la figura humana</strong> – Antigua Academia de San Carlos (2019).</li>
    </ul>

    <h3 class="section-divider">Gestión de Estudio & Proyectos</h3>
    <p>
      Desde 2018, lidero mi propio estudio como <strong>Artista Visual y Gestora de Proyectos</strong>, gestionando la administración de marca, la relación con coleccionistas y la curaduría de piezas certificadas.
    </p>
  </div>

  <div class="back-container">
    <a href="{{ site.baseurl }}/" class="btn-back">← Volver al inicio</a>
  </div>
</div>

---
layout: default
title: Verificación
description: Consulta el registro público de certificados de autenticidad de Nanitre.
---

<section class="verify-page">
  <div>
    <p class="eyebrow">Registro público Nanitre</p>
    <h1 class="display">Verifica la<br>autenticidad de<br>una <em>obra.</em></h1>
    <p class="verify-page__intro">Cada pieza registrada por el estudio cuenta con un identificador único. Introduce el código completo para consultar su ficha.</p>

    <form class="verify-form" id="verifyForm">
      <label class="skip-link" for="certId">Identificador del certificado</label>
      <input type="text" id="certId" name="certId" placeholder="DT-2024-003" autocomplete="off" autocapitalize="characters" spellcheck="false" required>
      <button type="submit">Consultar <span aria-hidden="true">↗</span></button>
    </form>
    <p class="verify-help">El identificador aparece en el certificado físico o digital entregado con la pieza.</p>
  </div>

  <aside class="verify-side">
    <div class="verify-side__number" aria-hidden="true">01</div>
    <h2>Un registro claro y trazable</h2>
    <p>La consulta confirma que el identificador coincide con el archivo público del estudio. Incluye título, técnica, año y estado de la pieza.</p>
    <p>Este registro acompaña al certificado de autenticidad; no sustituye la documentación original.</p>
  </aside>
</section>

<div class="result-overlay" id="modalResultado" aria-hidden="true">
  <section class="result-card" role="dialog" aria-modal="true" aria-labelledby="resultTitle">
    <button class="result-close" id="closeResult" type="button" aria-label="Cerrar resultado">×</button>
    <div id="resultadoContenido" aria-live="polite"></div>
  </section>
</div>

<script>
  const certificateDatabase = [
    {% for cert in site.data.certificados %}
    {
      id: "{{ cert.id | upcase }}",
      titulo: "{{ cert.titulo }}",
      tecnica: "{{ cert.tecnica }}",
      propietario: "{{ cert.propietario }}",
      fecha: "{{ cert.anio }}",
      estado: "{{ cert.estado }}",
      imagen: "{{ cert.imagen | replace: '/nanitre', '' | relative_url }}"
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  const form = document.getElementById("verifyForm");
  const input = document.getElementById("certId");
  const modal = document.getElementById("modalResultado");
  const result = document.getElementById("resultadoContenido");
  const closeButton = document.getElementById("closeResult");

  function openResult() {
    modal.classList.add("active");
    modal.setAttribute("aria-hidden", "false");
    document.body.style.overflow = "hidden";
    closeButton.focus();
  }

  function closeResult() {
    modal.classList.remove("active");
    modal.setAttribute("aria-hidden", "true");
    document.body.style.overflow = "";
    input.select();
  }

  form.addEventListener("submit", function (event) {
    event.preventDefault();
    const query = input.value.trim().toUpperCase();
    if (!query) return;

    const piece = certificateDatabase.find(function (item) { return item.id === query; });

    if (piece) {
      result.innerHTML =
        '<span class="result-status">✓ Registro verificado</span>' +
        '<h2 id="resultTitle">' + piece.titulo + '</h2>' +
        '<img class="result-artwork" src="' + piece.imagen + '" alt="Obra: ' + piece.titulo + '">' +
        '<div class="result-table">' +
          '<div class="result-row"><span>Técnica</span><strong>' + piece.tecnica + '</strong></div>' +
          '<div class="result-row"><span>Año de registro</span><strong>' + piece.fecha + '</strong></div>' +
          '<div class="result-row"><span>Estado</span><strong>' + piece.estado + '</strong></div>' +
          '<div class="result-row"><span>Disponibilidad</span><strong>' + piece.propietario + '</strong></div>' +
        '</div>' +
        '<div class="result-code">REGISTRO NANITRE · ' + piece.id + '</div>';
    } else {
      result.innerHTML =
        '<div class="result-invalid">' +
          '<div class="result-invalid__mark" aria-hidden="true">×</div>' +
          '<span class="eyebrow">Consulta sin coincidencias</span>' +
          '<h2 id="resultTitle">El código no aparece en el registro.</h2>' +
          '<p>Comprueba los caracteres del identificador e intenta nuevamente. Si el código pertenece a una pieza adquirida, contacta con el estudio.</p>' +
        '</div>';
    }
    openResult();
  });

  closeButton.addEventListener("click", closeResult);
  modal.addEventListener("click", function (event) {
    if (event.target === modal) closeResult();
  });
  document.addEventListener("keydown", function (event) {
    if (event.key === "Escape" && modal.classList.contains("active")) closeResult();
  });
</script>
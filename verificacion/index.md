---
layout: default
title: Verificación de Autenticidad
---

<section style="max-width: 600px; margin: 4rem auto; text-align: center; padding: 0 1rem;">
    <h2 style="font-weight: 300; letter-spacing: -1px; font-size: 2.5rem; margin-bottom: 1rem;">Verificar Obra</h2>
    <p style="color: var(--secondary-color); font-size: 1rem; margin-bottom: 3rem; line-height: 1.6;">
        Introduce el ID único del certificado para validar la integridad y procedencia de la pieza.
    </p>

    <div style="display: flex; flex-direction: column; gap: 15px; margin-bottom: 3rem;">
        <input type="text" id="certId" placeholder="Ej: DT-2024-001" 
            style="padding: 1.2rem; border: 1px solid #e0e0e0; border-radius: 4px; outline: none; font-family: inherit; font-size: 1rem; text-align: center; text-transform: uppercase;">
        <button onclick="verificar()" 
            style="background: var(--primary-color); color: white; border: none; padding: 1.2rem; cursor: pointer; border-radius: 4px; font-weight: 600; letter-spacing: 1px; transition: opacity 0.3s;">
            CONSULTAR REGISTRO
        </button>
    </div>

    <div id="resultado" style="display: none; text-align: left; padding: 2.5rem; border: 1px solid #eee; border-radius: 8px; background-color: #fcfcfc; box-shadow: 0 4px 20px rgba(0,0,0,0.02);">
    </div>
</section>

<script>
    const database = [
        {% for cert in site.data.certificados %}
        {
            "id": "{{ cert.id }}",
            "titulo": "{{ cert.titulo }}",
            "propietario": "{{ cert.propietario }}",
            "fecha": "{{ cert.fecha_emision }}",
            "estado": "{{ cert.estado }}"
        }{% unless forloop.last %},{% endunless %}
        {% endfor %}
    ];

    function verificar() {
        const idBusqueda = document.getElementById('certId').value.trim().toUpperCase();
        const contenedor = document.getElementById('resultado');
        const pieza = database.find(item => item.id === idBusqueda);

        contenedor.style.display = 'block';

        if (pieza) {
            contenedor.innerHTML = `
                <div style="border-bottom: 1px solid #eee; padding-bottom: 1.5rem; margin-bottom: 1.5rem; text-align: center;">
                    <span style="color: #27ae60; font-weight: 600; font-size: 0.9rem; text-transform: uppercase; letter-spacing: 2px;">✓ Certificado Válido</span>
                </div>
                <div style="display: grid; gap: 1rem; font-size: 0.95rem;">
                    <p style="margin:0;"><strong>Título de la Obra:</strong> <span style="color: #444;">${pieza.titulo}</span></p>
                    <p style="margin:0;"><strong>Estado de Propiedad:</strong> <span style="color: #444;">${pieza.propietario}</span></p>
                    <p style="margin:0;"><strong>Fecha de Registro:</strong> <span style="color: #444;">${pieza.fecha}</span></p>
                    <p style="margin:0;"><strong>Condición:</strong> <span style="color: #444;">${pieza.estado}</span></p>
                </div>
                <div style="margin-top: 2rem; padding-top: 1.5rem; border-top: 1px solid #eee; font-size: 0.8rem; color: #999; text-align: center;">
                    Registro oficial Nanitre ID: ${pieza.id}
                </div>
            `;
        } else {
            contenedor.innerHTML = `
                <div style="text-align: center; color: #e74c3c;">
                    <p style="font-weight: 600; margin-bottom: 0.5rem;">ID no reconocido</p>
                    <p style="font-size: 0.85rem; color: #888; margin: 0;">Por favor, verifica que el código coincida con el de tu certificado físico o contacta a soporte.</p>
                </div>
            `;
        }
    }
</script>

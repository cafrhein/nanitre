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
</section>

<div id="modalResultado" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.5); backdrop-filter: blur(4px);">
    <div style="position: relative; background-color: #fcfcfc; margin: 10% auto; padding: 2.5rem; border: 1px solid #eee; border-radius: 8px; width: 90%; max-width: 500px; box-shadow: 0 4px 20px rgba(0,0,0,0.15);">
        
        <span onclick="cerrarModal()" style="position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; color: #999;">&times;</span>
        
        <div id="resultadoContenido" style="text-align: left;">
            </div>

        <button onclick="cerrarModal()" style="margin-top: 2rem; width: 100%; background: #f0f0f0; color: #333; border: none; padding: 0.8rem; cursor: pointer; border-radius: 4px; font-size: 0.9rem;">
            CERRAR
        </button>
    </div>
</div>

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
        const input = document.getElementById('certId');
        const idBusqueda = input.value.trim().toUpperCase();
        const modal = document.getElementById('modalResultado');
        const contenedor = document.getElementById('resultadoContenido');
        
        if (idBusqueda === "") return;

        const pieza = database.find(item => item.id === idBusqueda);

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
                <div style="text-align: center; color: #e74c3c; padding: 1rem 0;">
                    <p style="font-weight: 600; margin-bottom: 0.5rem;">ID no reconocido</p>
                    <p style="font-size: 0.85rem; color: #888; margin: 0;">Por favor, verifica que el código coincida con el de tu certificado físico o contacta a soporte.</p>
                </div>
            `;
        }
        
        modal.style.display = 'block';
    }

    function cerrarModal() {
        const modal = document.getElementById('modalResultado');
        const input = document.getElementById('certId');
        const contenedor = document.getElementById('resultadoContenido');

        modal.style.display = 'none';
        // Limpiamos los campos para la siguiente consulta
        input.value = "";
        contenedor.innerHTML = "";
    }

    // Cerrar al hacer clic fuera del contenido blanco
    window.onclick = function(event) {
        const modal = document.getElementById('modalResultado');
        if (event.target == modal) {
            cerrarModal();
        }
    }
</script>

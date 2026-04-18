---
layout: default
title: Verificación de Autenticidad
---

<section style="max-width: 600px; margin: 4rem auto; text-align: center;">
    <h2 style="font-weight: 300; letter-spacing: -1px; font-size: 2rem;">Verificar Obra</h2>
    <p style="color: var(--secondary-color); font-size: 0.9rem; margin-bottom: 2rem;">
        Introduce el ID único del certificado para validar la autenticidad de la pieza.
    </p>

    <div style="display: flex; gap: 10px; margin-bottom: 3rem;">
        <input type="text" id="certId" placeholder="Ej: DT-2024-001" 
            style="flex: 1; padding: 1rem; border: 1px solid #e0e0e0; border-radius: 0; outline: none; font-family: inherit;">
        <button onclick="verificar()" 
            style="background: var(--primary-color); color: white; border: none; padding: 0 2rem; cursor: pointer; transition: opacity 0.3s;">
            Consultar
        </button>
    </div>

    <div id="resultado" style="text-align: left; padding: 2rem; border: 1px solid #f0f0f0; display: none;">
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
                <h3 style="margin-top:0; color: #27ae60;">✓ Registro Encontrado</h3>
                <p><strong>Obra:</strong> ${pieza.titulo}</p>
                <p><strong>Coleccionista:</strong> ${pieza.propietario}</p>
                <p><strong>Fecha de Emisión:</strong> ${pieza.fecha}</p>
                <p><strong>Estado:</strong> ${pieza.estado}</p>
            `;
        } else {
            contenedor.innerHTML = `
                <p style="color: #e74c3c; margin: 0;">ID no encontrado. Por favor, verifica los caracteres o contacta a soporte.</p>
            `;
        }
    }
</script>

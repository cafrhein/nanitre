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

<div id="modalResultado" style="display: none; position: fixed; z-index: 9999; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.6); backdrop-filter: blur(8px); display: none; align-items: center; justify-content: center; padding: 20px; box-sizing: border-box;">
    
    <div style="position: relative; background-color: #ffffff; padding: 2.5rem; border-radius: 12px; width: 100%; max-width: 500px; max-height: 90vh; overflow-y: auto; box-shadow: 0 20px 40px rgba(0,0,0,0.2); animation: modalFadeIn 0.3s ease-out;">
        
        <span onclick="cerrarModal()" style="position: absolute; top: 15px; right: 20px; font-size: 1.8rem; cursor: pointer; color: #ccc; line-height: 1; transition: color 0.2s;" onmouseover="this.style.color='#000'" onmouseout="this.style.color='#ccc'">&times;</span>
        
        <div id="resultadoContenido" style="text-align: left;">
            </div>

        <button onclick="cerrarModal()" style="margin-top: 2rem; width: 100%; background: #f5f5f5; color: #333; border: none; padding: 1rem; cursor: pointer; border-radius: 6px; font-size: 0.9rem; font-weight: 600; transition: background 0.2s;" onmouseover="this.style.background='#eee'" onmouseout="this.style.background='#f5f5f5'">
            CERRAR
        </button>
    </div>
</div>

<style>
    /* Animación de entrada para suavidad UX */
    @keyframes modalFadeIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }

    /* Ajuste visual del modal cuando está activo */
    #modalResultado.active {
        display: flex !important;
    }
</style>

<script>
    const database = [
        {% for cert in site.data.certificados %}
        {
            "id": "{{ cert.id }}",
            "titulo": "{{ cert.titulo }}",
            "propietario": "{{ cert.propietario }}",
            "fecha": "{{ cert.anio }}",
            "estado": "{{ cert.estado }}",
            "imagen": "{{ cert.imagen }}"
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
                <div style="border-bottom: 1px solid #f0f0f0; padding-bottom: 1.5rem; margin-bottom: 1.5rem; text-align: center;">
                    <img src="${pieza.imagen}" alt="${pieza.titulo}" style="width: 100%; max-height: 280px; object-fit: contain; margin-bottom: 1.5rem; border-radius: 4px; background: #f9f9f9;">
                    <div style="display: inline-block; padding: 4px 12px; background: #eafff2; border-radius: 20px; margin-bottom: 10px;">
                        <span style="color: #27ae60; font-weight: 600; font-size: 0.75rem; text-transform: uppercase; letter-spacing: 1px;">✓ Certificado Válido</span>
                    </div>
                    <h3 style="margin: 10px 0 0; font-size: 1.4rem; font-weight: 600;">${pieza.titulo}</h3>
                </div>
                <div style="display: grid; gap: 0.8rem; font-size: 0.9rem; color: #666;">
                    <p style="margin:0; display: flex; justify-content: space-between;"><strong style="color: #000;">Propietario:</strong> <span>${pieza.propietario}</span></p>
                    <p style="margin:0; display: flex; justify-content: space-between;"><strong style="color: #000;">Año de Registro:</strong> <span>${pieza.fecha}</span></p>
                    <p style="margin:0; display: flex; justify-content: space-between;"><strong style="color: #000;">Estado:</strong> <span>${pieza.estado}</span></p>
                </div>
                <div style="margin-top: 2rem; padding: 1rem; background: #fcfcfc; border: 1px dashed #ddd; border-radius: 6px; font-size: 0.75rem; color: #999; text-align: center; font-family: monospace;">
                    REGISTRO OFICIAL NANITRE ID: ${pieza.id}
                </div>
            `;
        } else {
            contenedor.innerHTML = `
                <div style="text-align: center; padding: 2rem 0;">
                    <div style="font-size: 3rem; margin-bottom: 1rem;">⚠️</div>
                    <p style="font-weight: 600; color: #000; margin-bottom: 0.5rem; font-size: 1.1rem;">ID No Encontrado</p>
                    <p style="font-size: 0.9rem; color: #777; margin: 0; line-height: 1.5;">El código no coincide con nuestros registros de autenticidad. Por favor, revisa el certificado físico.</p>
                </div>
            `;
        }
        
        modal.classList.add('active');
    }

    function cerrarModal() {
        const modal = document.getElementById('modalResultado');
        modal.classList.remove('active');
    }

    // Cerrar al hacer clic fuera del contenido blanco
    window.onclick = function(event) {
        const modal = document.getElementById('modalResultado');
        if (event.target == modal) {
            cerrarModal();
        }
    }
</script>

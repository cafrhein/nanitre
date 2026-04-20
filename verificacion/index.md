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
        <input type="text" id="certId" placeholder="Ej: DT-2024-003" 
            style="padding: 1.2rem; border: 1px solid #e0e0e0; border-radius: 4px; outline: none; font-family: inherit; font-size: 1rem; text-align: center; text-transform: uppercase;">
        <button onclick="verificar()" 
            style="background: var(--primary-color); color: white; border: none; padding: 1.2rem; cursor: pointer; border-radius: 4px; font-weight: 600; letter-spacing: 1px; transition: opacity 0.3s;">
            CONSULTAR REGISTRO
        </button>
    </div>
</section>

<div id="modalResultado" class="modal-overlay">
    <div class="modal-card">
        <span onclick="cerrarModal()" class="close-icon">&times;</span>
        
        <div id="resultadoContenido">
            </div>

        <button onclick="cerrarModal()" class="btn-modal-close">CERRAR</button>
    </div>
</div>

<style>
    .modal-overlay {
        display: none;
        position: fixed;
        z-index: 9999;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(255,255,255,0.9);
        backdrop-filter: blur(10px);
        align-items: center;
        justify-content: center;
        padding: 20px;
        box-sizing: border-box;
    }

    .modal-overlay.active {
        display: flex !important;
    }

    .modal-card {
        position: relative;
        background-color: #ffffff;
        padding: 2.5rem;
        border-radius: 8px;
        width: 100%;
        max-width: 550px;
        box-shadow: 0 40px 100px rgba(0,0,0,0.1);
        animation: modalSlideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        text-align: center;
    }

    @keyframes modalSlideUp {
        from { opacity: 0; transform: translateY(30px); }
        to { opacity: 1; transform: translateY(0); }
    }

    .close-icon {
        position: absolute;
        top: 20px;
        right: 20px;
        font-size: 2rem;
        cursor: pointer;
        color: #ddd;
        font-weight: 300;
    }

    .badge-valid {
        display: inline-flex;
        align-items: center;
        gap: 5px;
        background: #eafff2;
        color: #27ae60;
        padding: 6px 16px;
        border-radius: 4px;
        font-size: 0.7rem;
        font-weight: 600;
        text-transform: uppercase;
        letter-spacing: 1px;
        margin-bottom: 2rem;
    }

    .cert-title {
        font-size: 1.8rem;
        font-weight: 400;
        margin: 0 0 2rem 0;
        letter-spacing: -0.5px;
    }

    .info-table {
        width: 100%;
        margin-bottom: 2.5rem;
        border-top: 1px solid #f0f0f0;
    }

    .info-row {
        display: flex;
        justify-content: space-between;
        padding: 1rem 0;
        border-bottom: 1px solid #f0f0f0;
        font-size: 0.95rem;
    }

    .info-label { color: #000; font-weight: 400; }
    .info-value { color: #888; }

    .id-footer-badge {
        margin-top: 1rem;
        padding: 1.2rem;
        border: 1px dashed #e0e0e0;
        border-radius: 4px;
        font-family: monospace;
        font-size: 0.75rem;
        color: #aaa;
        letter-spacing: 1px;
    }

    .btn-modal-close {
        margin-top: 2rem;
        width: 100%;
        background: #f8f8f8;
        color: #000;
        border: none;
        padding: 1.2rem;
        cursor: pointer;
        border-radius: 4px;
        font-size: 0.85rem;
        font-weight: 600;
        letter-spacing: 1px;
        transition: background 0.2s;
    }

    .btn-modal-close:hover { background: #f0f0f0; }
</style>

<script>
    // Generación dinámica de la base de datos desde Jekyll
    const database = [
        {% for cert in site.data.certificados %}
        {
            "id": "{{ cert.id | upcase }}",
            "titulo": "{{ cert.titulo }}",
            "propietario": "{{ cert.propietario }}",
            "fecha": "{{ cert.anio }}",
            "estado": "{{ cert.estado }}",
            "imagen": "{{ cert.imagen | relative_url }}"
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
                <div class="badge-valid">✓ Certificado Válido</div>
                <h3 class="cert-title">${pieza.titulo}</h3>
                
                <div class="info-table">
                    <div class="info-row">
                        <span class="info-label">Propietario:</span>
                        <span class="info-value">${pieza.propietario}</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">Año de Registro:</span>
                        <span class="info-value">${pieza.fecha}</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">Estado:</span>
                        <span class="info-value">${pieza.estado}</span>
                    </div>
                </div>

                <div class="id-footer-badge">
                    REGISTRO OFICIAL NANITRE ID: ${pieza.id}
                </div>
            `;
        } else {
            contenedor.innerHTML = `
                <div style="padding: 2rem 0;">
                    <div style="font-size: 2rem; margin-bottom: 1rem;">✕</div>
                    <h3 style="font-weight: 600; margin-bottom: 0.5rem;">ID NO ENCONTRADO</h3>
                    <p style="font-size: 0.9rem; color: #888; line-height: 1.6;">
                        El código no coincide con nuestros registros oficiales.<br>
                        Por favor, verifica los caracteres e intenta de nuevo.
                    </p>
                </div>
            `;
        }
        
        modal.classList.add('active');
    }

    function cerrarModal() {
        document.getElementById('modalResultado').classList.remove('active');
    }

    window.onclick = function(event) {
        const modal = document.getElementById('modalResultado');
        if (event.target == modal) cerrarModal();
    }
</script>

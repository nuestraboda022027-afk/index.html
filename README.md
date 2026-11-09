<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nuestra Boda</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #fdfbf7; color: #333; text-align: center; padding: 40px; }
        form { background: white; max-width: 400px; margin: 0 auto; padding: 30px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); text-align: left; }
        input, select, textarea { width: 100%; padding: 10px; margin: 8px 0 20px 0; border: 1px solid #ddd; border-radius: 6px; box-sizing: border-box; }
        button { background: #d4af37; color: white; border: none; padding: 12px; width: 100%; border-radius: 6px; font-size: 16px; cursor: pointer; }
        button:hover { background: #b89728; }
    </style>
</head>
<body>

    <h1>¡Nos Casamos!</h1>
    <p>Estefany & Daniel - 2026</p>
    <p>Por favor confirma tu asistencia llenando el siguiente formulario:</p>

    <!-- Formulario que apunta a tu Google Apps Script -->
    <form id="rsvp-form">
        <label for="Nombre">Nombre completo:</label>
        <input type="text" id="Nombre" name="Nombre" required>

        <label for="Asistencia">¿Nos acompañaras?</label>
        <select id="Asistencia" name="Asistencia">
            <option value="Sí">Sí, ahí estaré</option>
            <option value="No">No podré asistir</option>
        </select>

        <label for="Acompañantes">Número de acompañantes:</label>
        <input type="number" id="Acompañantes" name="Acompañantes" value="0" min="0">

        <label for="Mensaje">Mensaje para los novios:</label>
        <textarea id="Mensaje" name="Mensaje" rows="3"></textarea>

        <button type="submit" id="btn-enviar">Confirmar Asistencia</button>
    </form>

    <div id="mensaje-exito" style="display:none; color: green; margin-top: 20px;">
        <h3>¡Gracias por confirmar! Hemos guardado tu respuesta.</h3>
    </div>

    <script>
        const scriptURL = 'PEGAR_AQUI_TU_URL_DE_GOOGLE_APPS_SCRIPT';
        const form = document.getElementById('rsvp-form');
        const mensajeExito = document.getElementById('mensaje-exito');

        form.addEventListener('submit', e => {
            e.preventDefault();
            document.getElementById('btn-enviar').disabled = true;
            document.getElementById('btn-enviar').innerText = 'Enviando...';

            fetch(scriptURL, { method: 'POST', body: new FormData(form)})
                .then(response => {
                    form.style.display = 'none';
                    mensajeExito.style.display = 'block';
                })
                .catch(error => {
                    console.error('Error!', error.message);
                    alert('Hubo un error al enviar. Por favor intenta de nuevo.');
                    document.getElementById('btn-enviar').disabled = false;
                    document.getElementById('btn-enviar').innerText = 'Confirmar Asistencia';
                });
        });
    </script>

</body>
</html>

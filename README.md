# Boda-Maria-y-Freddy
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boda María & Freddy</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Playfair+Display:ital@0;1&family=Montserrat:wght@300;400&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/scrollreveal@4.0.9/dist/scrollreveal.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    
    <style>
        :root {
            --oro: #b4975a;
            --crema: #f9f7f2;
            --vino: #630d16;
            --texto: #333;
        }

        body, html { margin: 0; padding: 0; background: var(--crema); font-family: 'Montserrat', sans-serif; overflow: hidden; height: 100%; width: 100%; }

        /* Capa superior del sobre */
        #envelope-container {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #e8e2d6; z-index: 9999; display: flex; flex-direction: column;
            justify-content: center; align-items: center; cursor: pointer;
        }

        .envelope {
            position: relative; width: 320px; height: 200px; background: #fffcf5;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2); border-radius: 4px;
        }

        /* La solapa (triangulito de arriba) */
        .flap {
            position: absolute; top: 0; left: 0; width: 0; height: 0;
            border-left: 160px solid transparent; border-right: 160px solid transparent;
            border-top: 110px solid #dcd3c1; transform-origin: top; transition: transform 0.6s; z-index: 3;
        }

        /* Sello de lacre */
        .seal {
            position: absolute; top: 85px; left: 50%; transform: translateX(-50%);
            width: 55px; height: 55px; background: var(--vino); border-radius: 50%;
            z-index: 4; display: flex; align-items: center; justify-content: center;
            color: var(--oro); font-family: 'Cinzel', serif; font-weight: bold;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3); transition: 0.4s; border: 2px solid #80101b;
        }

        /* Clase que activa la apertura */
        .open-envelope .flap { transform: rotateX(180deg); z-index: 1; }
        .open-envelope .seal { opacity: 0; transform: translateX(-50%) scale(0); }

        /* Contenido de la invitación */
        #main-content { opacity: 0; transition: 1.2s; background: var(--crema); }
        
        section { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 40px; text-align: center; }
        h1 { font-family: 'Cinzel', serif; font-size: 2.5rem; color: var(--oro); margin: 10px 0; }
        .btn {
            display: inline-block; padding: 12px 30px; margin: 10px; border: 1px solid var(--oro);
            color: var(--oro); text-decoration: none; text-transform: uppercase; letter-spacing: 2px;
        }
    </style>
</head>
<body onclick="abrirTodo()"> <div id="envelope-container">
        <div class="envelope" id="miSobre">
            <div class="flap"></div>
            <div class="seal">M&F</div>
        </div>
        <p style="margin-top: 40px; font-family: 'Cinzel'; color: #8a765a; letter-spacing: 2px;">Toca para abrir la invitación</p>
    </div>

    <div id="main-content">
        <section>
            <div class="reveal">
                <p>NUESTRA BODA</p>
                <h1>María & Freddy</h1>
                <p style="font-family: 'Playfair Display'; font-style: italic; font-size: 1.3rem;">"Ambulancias forever"</p>
                <div style="border-top: 1px solid var(--oro); border-bottom: 1px solid var(--oro); padding: 10px 40px; margin: 20px 0;">
                    24 . 10 . 2026
                </div>
                <p><strong>Concatedral de Sta María la Redonda</strong></p>
            </div>
        </section>

        <section style="background-color: #fff;">
            <div class="reveal">
                <h2>¿Dónde y Cuándo?</h2>
                <p>La ceremonia comenzará a las 12:00h</p>
                <a href="#" class="btn">Mapa Logroño</a>
                <br><br>
                <h2>Confirmación</h2>
                <a href="#" class="btn">Confirmar WhatsApp</a>
            </div>
        </section>

        <section>
            <div class="reveal">
                <h2>Regalo y Música</h2>
                <button class="btn" onclick="alert('IBAN: ES00...')">Ver Cuenta Bancaria</button>
                <a href="#" class="btn">Elegir Música</a>
            </div>
        </section>
    </div>

    <script>
        function abrirTodo() {
            const sobre = document.getElementById('miSobre');
            const contenedor = document.getElementById('envelope-container');
            const contenido = document.getElementById('main-content');

            // 1. Animamos el sobre
            sobre.classList.add('open-envelope');

            // 2. Tiramos confeti (solo si hay internet para cargar la librería)
            if (typeof confetti === "function") {
                confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 } });
            }

            // 3. Desaparece el sobre y aparece la web
            setTimeout(() => {
                contenedor.style.opacity = '0';
                contenedor.style.pointerEvents = 'none'; // Para poder hacer scroll
                contenido.style.opacity = '1';
                document.body.style.overflow = 'auto'; // Permitir scroll
            }, 800);
        }

        // Animación de los textos al bajar
        ScrollReveal().reveal('.reveal', { 
            distance: '50px', duration: 1000, origin: 'bottom', interval: 200 
        });
    </script>
</body>
</html>

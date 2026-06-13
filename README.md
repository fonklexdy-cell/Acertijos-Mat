
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Acertijos Mat </title>
    <style>
        :root {
            --amarillo: #FFD166;
            --azul: #118AB2;
            --verde: #06D6A0;
            --naranja: #F77F00;
            --rosa: #EF476F;
            --rojo: #D90429;
            --oscuro: #073B4C;
            --blanco: #FFFFFF;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--azul), var(--oscuro));
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: var(--oscuro);
            padding: 15px;
            overflow-x: hidden;
        }

        .contenedor-juego {
            background-color: var(--blanco);
            width: 100%;
            max-width: 650px;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            overflow: hidden;
            text-align: center;
            padding: 30px;
            position: relative;
        }

        /* Pantallas con Animación de Entrada */
        .pantalla {
            display: none;
            opacity: 0;
            transform: translateX(50px);
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .pantalla.activa {
            display: flex;
            flex-direction: column;
            gap: 20px;
            align-items: center;
            opacity: 1;
            transform: translateX(0);
        }

        h1 {
            color: var(--naranja);
            font-size: 2.5rem;
            text-shadow: 3px 3px var(--amarillo);
            margin-bottom: 10px;
            animation: flotar 3s ease-in-out infinite;
        }

        p {
            font-size: 1.2rem;
            color: var(--oscuro);
            font-weight: 600;
        }

        .marcador-contenedor {
            display: flex;
            justify-content: space-between;
            width: 100%;
            background-color: #f0f4f8;
            padding: 12px 25px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 1.1rem;
            border: 3px solid var(--azul);
        }

        .tiempo-alerta {
            color: var(--rojo);
            animation: pulso 0.4s infinite alternate;
        }

        .avatar-contenedor {
            width: 130px;
            height: 130px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 4.5rem;
            background-color: var(--amarillo);
            border: 6px solid var(--blanco);
            box-shadow: 0 8px 20px rgba(0,0,0,0.15);
            transition: transform 0.3s ease;
        }

        .burbuja-texto {
            background-color: #f0f4f8;
            padding: 15px 20px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 1.1rem;
            max-width: 90%;
            border: 3px solid #ddd;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .cuadro-acertijo {
            font-size: 1.25rem;
            font-weight: 700;
            padding: 20px;
            border-radius: 22px;
            background-color: #f8f9fa;
            border: 4px dashed var(--naranja);
            width: 100%;
            line-height: 1.5;
            box-shadow: inset 0 2px 10px rgba(0,0,0,0.05);
        }

        .opciones-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            width: 100%;
        }

        .btn {
            color: var(--blanco);
            border: none;
            padding: 16px 20px;
            font-size: 1.25rem;
            font-weight: bold;
            border-radius: 18px;
            cursor: pointer;
            transition: transform 0.1s, filter 0.2s;
            box-shadow: 0 6px 0px rgba(0,0,0,0.2);
            width: 100%;
        }

        .btn:active {
            transform: translateY(6px);
            box-shadow: none;
        }

        .btn:hover {
            filter: brightness(1.1);
        }

        .btn-inicio { background-color: var(--verde); font-size: 1.5rem; padding: 20px; }
        .btn-reinicio { background-color: var(--rosa); }
        
        .opciones-grid .btn:nth-child(1) { background-color: var(--azul); }
        .opciones-grid .btn:nth-child(2) { background-color: var(--naranja); }
        .opciones-grid .btn:nth-child(3) { background-color: var(--rosa); }
        .opciones-grid .btn:nth-child(4) { background-color: var(--rojo); }

        .medalla {
            font-size: 6.5rem;
            animation: flotar 2.5s ease-in-out infinite;
        }

        .tabla-resultados {
            width: 100%;
            margin: 20px 0;
            border-collapse: collapse;
            font-size: 1.1rem;
        }

        .tabla-resultados th, .tabla-resultados td {
            padding: 12px;
            border-bottom: 2px solid #eee;
        }

        @keyframes pulso {
            from { transform: scale(1); }
            to { transform: scale(1.06); }
        }

        @keyframes flotar {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-12px); }
            100% { transform: translateY(0px); }
        }

        @media (max-width: 500px) {
            h1 { font-size: 2rem; }
            .cuadro-acertijo { font-size: 1.1rem; padding: 15px; }
            .opciones-grid { grid-template-columns: 1fr; }
            .avatar-contenedor { width: 100px; height: 100px; font-size: 3.5rem; }
            .contenedor-juego { padding: 15px; }
        }
    </style>
</head>
<body>

    <div class="contenedor-juego">
        
        <!-- PANTALLA INICIO -->
        <div id="pantalla-inicio" class="pantalla activa">
            <h1>Acertijos Mat</h1>
            <p>¡Resuelve los 8 acertijos del laberinto! Los aciertos suman puntos y los fallos restan. ¡Cuidado con el reloj!</p>
            <div style="font-size: 6rem; margin: 15px 0;">🧩🧙‍♂️🏰</div>
            <button class="btn btn-inicio" onclick="iniciarJuego()">¡COMENZAR DESAFÍO!</button>
        </div>

        <!-- PANTALLA JUEGO -->
        <div id="pantalla-juego" class="pantalla">
            <div class="marcador-contenedor">
                <div>Reto: <span id="ronda-actual">1</span>/8</div>
                <div>Nota: <span id="puntos">0</span>%</div>
                <div id="cronometro-box">Tiempo: <span id="tiempo">30</span>s</div>
            </div>

            <div class="avatar-contenedor" id="avatar">🧙‍♂️</div>
            <div class="burbuja-texto" id="burbuja">¡Es hora de pensar, tú puedes!</div>

            <!-- Contenedor del Acertijo de Texto -->
            <div class="cuadro-acertijo" id="bloque-acertijo">Cargando acertijo matemático...</div>

            <div class="opciones-grid" id="contenedor-opciones">
                <!-- Botones de opciones inyectados por JavaScript -->
            </div>
        </div>

        <!-- PANTALLA FINAL -->
        <div id="pantalla-final" class="pantalla">
            <h1>Resultados</h1>
            <div class="medalla" id="logro-medalla">🥇</div>
            <h2 id="logro-titulo">¡Evaluando!</h2>
            <p id="logro-descripcion">Cargando tu rendimiento...</p>
            
            <table class="tabla-resultados">
                <thead>
                    <tr>
                        <th style="text-align: left;">Métrica</th>
                        <th style="text-align: right;">Resultado</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td style="text-align: left;">Acertijos Totales</td>
                        <td style="text-align: right;">8</td>
                    </tr>
                    <tr>
                        <td style="text-align: left;">Respuestas Correctas</td>
                        <td id="res-correctas" style="text-align: right; color: var(--verde); font-weight: bold;">0</td>
                    </tr>
                    <tr>
                        <td style="text-align: left;">Respuestas Incorrectas</td>
                        <td id="res-incorrectas" style="text-align: right; color: var(--rojo); font-weight: bold;">0</td>
                    </tr>
                    <tr>
                        <td style="text-align: left;">Puntaje Final</td>
                        <td id="res-nota" style="text-align: right; font-weight: bold; color: var(--azul);">0%</td>
                    </tr>
                </tbody>
            </table>

            <button class="btn btn-reinicio" onclick="iniciarJuego()">REINTENTAR (Nuevos Retos)</button>
        </div>

    </div>

    <script>
        // Variables de estado del juego
        let puntosBase = 0;
        let tiempoRestante = 30;
        let temporizador = null;
        let respuestaCorrecta = 0;
        let correctasContadas = 0;
        let incorrectasContadas = 0;
        let totalPreguntas = 0;
        const maxPreguntas = 8;
        let acertijosActuales = [];

        // Banco de los 8 acertijos con sus respectivos avatares y colores temáticos
        const bancoAcertijos = [
            { txt: "Un mago plantó un árbol con 45 manzanas rojas. Al día siguiente, usó un hechizo y aparecieron 38 manzanas verdes más. ¿Cuántas manzanas tiene en total?", ans: 83, op: '+', avatar: '🧙‍♂️', color: 'var(--azul)' },
            { txt: "En una partida, Lucas recolectó 67 gemas azules en el primer nivel y 55 gemas amarillas en el segundo. ¿Cuántas gemas juntó al terminar?", ans: 122, op: '+', avatar: '🧝‍♂️', color: 'var(--amarillo)' },
            { txt: "Sofía infló 92 globos para la escuela. Sopló un viento muy fuerte y se volaron 34 globos. ¿Cuántos globos le quedaron para decorar?", ans: 58, op: '-', avatar: '🦄', color: 'var(--rosa)' },
            { txt: "Un cofre pirata tenía 75 monedas de chocolate. Si los tripulantes se comieron 47 chocolates en el viaje, ¿cuántos chocolates quedan?", ans: 28, op: '-', avatar: '🏴‍☠️', color: 'var(--rojo)' },
            { txt: "El panadero preparó 6 cajas de donas mágicas. Si cada caja contiene exactamente 8 donas, ¿cuántas donas tiene listas en total?", ans: 48, op: '*', avatar: '🤖', color: 'var(--naranja)' },
            { txt: "En un pequeño corral de la granja hay exactamente 9 vacas comiendo pasto. Sin contar personas, ¿cuántas patas de vaca hay en total?", ans: 36, op: '*', avatar: '🤠', color: 'var(--verde)' },
            { txt: "Diego tiene un frasco con 42 canicas y quiere repartirlas en partes iguales entre sus 6 mejores amigos. ¿Cuántas canicas recibe cada uno?", ans: 7, op: '/', avatar: '🧑‍🤝‍🧑', color: 'var(--azul)' },
            { txt: "Valentina tiene 54 soldados de plástico y quiere acomodarlos en filas perfectas poniendo 9 en cada una. ¿Cuántas filas completas forma?", ans: 6, op: '/', avatar: '🎖️', color: 'var(--naranja)' }
        ];

        let ctxAudio = null;

        function inicializarAudio() {
            if (!ctxAudio) {
                ctxAudio = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function reproducirSonido(tipo) {
            inicializarAudio();
            if (!ctxAudio) return;
            const osc = ctxAudio.createOscillator();
            const ganancia = ctxAudio.createGain();
            osc.connect(ganancia);
            ganancia.connect(ctxAudio.destination);
            const ahora = ctxAudio.currentTime;

            if (tipo === 'correcto') {
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(523.25, ahora); // C5
                osc.frequency.setValueAtTime(659.25, ahora + 0.08); // E5
                osc.frequency.setValueAtTime(783.99, ahora + 0.16); // G5
                ganancia.gain.setValueAtTime(0.3, ahora);
                ganancia.gain.exponentialRampToValueAtTime(0.01, ahora + 0.35);
                osc.start(ahora); osc.stop(ahora + 0.35);
            } else if (tipo === 'incorrecto') {
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(160, ahora);
                osc.frequency.linearRampToValueAtTime(90, ahora + 0.25);
                ganancia.gain.setValueAtTime(0.3, ahora);
                ganancia.gain.exponentialRampToValueAtTime(0.01, ahora + 0.25);
                osc.start(ahora); osc.stop(ahora + 0.25);
            } else if (tipo === 'final') {
                // Sonido final envolvente estéreo/armónico
                [261.63, 329.63, 392.00, 523.25].forEach((frec, idx) => {
                    const o = ctxAudio.createOscillator();
                    const g = ctxAudio.createGain();
                    o.connect(g); g.connect(ctxAudio.destination);
                    o.type = 'sine';
                    o.frequency.setValueAtTime(frec, ahora + (idx * 0.05));
                    o.frequency.exponentialRampToValueAtTime(frec * 2, ahora + 1.2);
                    g.gain.setValueAtTime(0.12, ahora);
                    g.gain.exponentialRampToValueAtTime(0.001, ahora + 1.8);
                    o.start(ahora); o.stop(ahora + 1.8);
                });
            }
        }
        function cambiarPantalla(idPantalla) {
            const pantallas = document.querySelectorAll('.pantalla');
            pantallas.forEach(p => {
                p.classList.remove('activa');
                p.style.opacity = '0';
                p.style.transform = 'translateX(-50px)';
            });
            
            const activa = document.getElementById(idPantalla);
            activa.classList.add('activa');
            setTimeout(() => {
                activa.style.opacity = '1';
                activa.style.transform = 'translateX(0)';
            }, 50);
        }

        function iniciarJuego() {
            inicializarAudio();
            puntosBase = 0;
            correctasContadas = 0;
            incorrectasContadas = 0;
            totalPreguntas = 0;
            
            // Cada reinicio mezcla los acertijos para que el orden sea totalmente diferente
            acertijosActuales = [...bancoAcertijos].sort(() => Math.random() - 0.5);
            
            actualizarMarcadorPorcentaje();
            cambiarPantalla('pantalla-juego');
            generarNuevaActividad();
        }

        function actualizarMarcadorPorcentaje() {
            // El puntaje se calcula en base estricta de 0 a 100% de manera dinámica
            let pct = Math.round((puntosBase / (maxPreguntas * 10)) * 100);
            if (pct < 0) pct = 0;
            if (pct > 100) pct = 100;
            document.getElementById('puntos').innerText = pct;
        }

        function generarNuevaActividad() {
            if (totalPreguntas >= maxPreguntas) {
                finalizarJuego();
                return;
            }

            const item = acertijosActuales[totalPreguntas];
            totalPreguntas++;
            
            document.getElementById('ronda-actual').innerText = totalPreguntas;
            tiempoRestante = 30;
            document.getElementById('tiempo').innerText = tiempoRestante;
            document.getElementById('cronometro-box').classList.remove('tiempo-alerta');

            document.getElementById('burbuja').innerText = "¡Lee con mucha atención!";
            document.getElementById('burbuja').style.color = 'var(--oscuro)';

            // Cargar avatar, fondo contextual e imágenes de texto correspondientes
            const avatarElem = document.getElementById('avatar');
            avatarElem.innerText = item.avatar;
            avatarElem.style.backgroundColor = item.color;

            document.getElementById('bloque-acertijo').innerText = item.txt;
            respuestaCorrecta = item.ans;

            // Generar distractores numéricos lógicos
            let opciones = [respuestaCorrecta];
            while (opciones.length < 4) {
                let desvio = respuestaCorrecta + (Math.floor(Math.random() * 12) - 6);
                if (desvio !== respuestaCorrecta && desvio > 0 && !opciones.includes(desvio)) {
                    opciones.push(desvio);
                }
            }
            opciones.sort(() => Math.random() - 0.5);

            const contenedorOpciones = document.getElementById('contenedor-opciones');
            contenedorOpciones.innerHTML = '';
            opciones.forEach(opc => {
                const boton = document.createElement('button');
                boton.className = 'btn';
                boton.innerText = opc;
                boton.onclick = () => verificarRespuesta(opc);
                contenedorOpciones.appendChild(boton);
            });

            if (temporizador) clearInterval(temporizador);
            temporizador = setInterval(() => {
                tiempoRestante--;
                document.getElementById('tiempo').innerText = tiempoRestante;
                
                if (tiempoRestante <= 7) {
                    document.getElementById('cronometro-box').classList.add('tiempo-alerta');
                }

                if (tiempoRestante <= 0) {
                    clearInterval(temporizador);
                    procesarFallo();
                }
            }, 1000);
        }

        function verificarRespuesta(seleccionada) {
            if (temporizador) clearInterval(temporizador);
            
            if (seleccionada === respuestaCorrecta) {
                puntosBase += 10; // Suma puntos reales
                correctasContadas++;
                actualizarMarcadorPorcentaje();
                
                reproducirSonido('correcto');
                document.getElementById('burbuja').innerText = "CORRECTO";
                document.getElementById('burbuja').style.color = "var(--verde)";
                
                setTimeout(generarNuevaActividad, 1200);
            } else {
                procesarFallo();
            }
        }

        function procesarFallo() {
            if (temporizador) clearInterval(temporizador);
            incorrectasContadas++;
            
            // Penalización: Resta puntos al equivocarse disminuyendo el porcentaje final
            puntosBase = Math.max(0, puntosBase - 5);
            actualizarMarcadorPorcentaje();
            
            reproducirSonido('incorrecto');
            document.getElementById('burbuja').innerText = "INCORRECTO VUELVE A INTENTARLO";
            document.getElementById('burbuja').style.color = "var(--rojo)";

            setTimeout(generarNuevaActividad, 1400);
        }

        function finalizarJuego() {
            if (temporizador) clearInterval(temporizador);
            cambiarPantalla('pantalla-final');
            reproducirSonido('final');

            let notaFinal = Math.round((puntosBase / (maxPreguntas * 10)) * 100);
            if (notaFinal < 0) notaFinal = 0;
            if (notaFinal > 100) notaFinal = 100;

            document.getElementById('res-correctas').innerText = correctasContadas;
            document.getElementById('res-incorrectas').innerText = incorrectasContadas;
            document.getElementById('res-nota').innerText = `${notaFinal}%`;

            const medalla = document.getElementById('logro-medalla');
            const titulo = document.getElementById('logro-titulo');
            const desc = document.getElementById('logro-descripcion');

            if (notaFinal === 100) {
                medalla.innerText = '👑';
                titulo.innerText = '¡Perfecto Absoluto! (100%)';
                desc.innerText = '¡Increíble! Has resuelto todos los acertijos matemáticos con precisión de maestro.';
            } else if (notaFinal >= 80) {
                medalla.innerText = '🥇';
                titulo.innerText = `Rango Sobresaliente (${notaFinal}%)`;
                desc.innerText = '¡Gran trabajo! Tienes una excelente velocidad de cálculo mental.';
            } else if (notaFinal >= 60) {
                medalla.innerText = '🥈';
                titulo.innerText = `Rango Aprobado (${notaFinal}%)`;
                desc.innerText = '¡Superado! Pasaste la prueba, pero ten cuidado de no confundirte para mantener tu nota alta.';
            } else {
                medalla.innerText = '🥉';
                titulo.innerText = `Rango Insuficiente (${notaFinal}%)`;
                desc.innerText = '¡Sigue intentándolo! Los errores bajaron tu puntaje. ¡Presiona reiniciar para volver a entrenar!';
            }
        }
    </script>
</body>
</html>

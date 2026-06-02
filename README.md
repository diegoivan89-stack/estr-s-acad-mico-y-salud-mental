<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mente Sana | Gestión del Estrés Académico</title>
    <style>
        :root {
            --primary: #4a90e2;
            --primary-dark: #357abd;
            --secondary: #2ecc71;
            --bg: #f5f7fa;
            --text: #2c3e50;
            --card-bg: #ffffff;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            --radius: 12px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }

        header {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            padding: 40px 20px;
            text-align: center;
            border-bottom-left-radius: var(--radius);
            border-bottom-right-radius: var(--radius);
            box-shadow: var(--shadow);
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        main {
            max-width: 1000px;
            margin: 30px auto;
            padding: 0 20px;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
            margin-bottom: 40px;
        }

        @media (min-width: 768px) {
            .grid {
                grid-template-columns: 1fr 1fr;
            }
        }

        .card {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            border-top: 5px solid var(--primary);
        }

        .card h2 {
            margin-bottom: 15px;
            color: var(--primary-dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        ul {
            list-style-position: inside;
            margin-left: 10px;
        }

        li {
            margin-bottom: 8px;
        }

        /* --- Widget Interactivo: Termómetro de Estrés --- */
        .widget-box {
            background-color: var(--card-bg);
            padding: 30px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            margin-bottom: 40px;
            border: 1px solid #e1e8ed;
        }

        .widget-box h2 {
            text-align: center;
            margin-bottom: 20px;
            color: var(--text);
        }

        .slider-container {
            margin: 30px 0;
            text-align: center;
        }

        .slider {
            -webkit-appearance: none;
            width: 100%;
            height: 12px;
            border-radius: 6px;
            background: #e1e8ed;
            outline: none;
            transition: background 0.3s;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: var(--primary);
            cursor: pointer;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
            transition: transform 0.1s;
        }

        .slider::-webkit-slider-thumb:hover {
            transform: scale(1.2);
        }

        .status-display {
            text-align: center;
            padding: 20px;
            border-radius: var(--radius);
            margin-top: 20px;
            font-weight: bold;
            font-size: 1.2rem;
            transition: all 0.4s ease;
        }

        /* --- Sección de Técnicas --- */
        .technique-btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: var(--radius);
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            margin-top: 15px;
            transition: background 0.2s;
        }

        .technique-btn:hover {
            background-color: var(--primary-dark);
        }

        .exercise-area {
            margin-top: 20px;
            padding: 20px;
            background-color: #f8fafc;
            border-radius: var(--radius);
            border-left: 4px solid var(--secondary);
            display: none;
            text-align: center;
        }

        .breathing-circle {
            width: 100px;
            height: 100px;
            background-color: var(--secondary);
            border-radius: 50%;
            margin: 20px auto;
            opacity: 0.8;
            transition: transform 4s ease-in-out;
        }

        .breathing-circle.expand {
            transform: scale(1.6);
        }

        footer {
            text-align: center;
            padding: 30px;
            color: #7f8c8d;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <header>
        <h1>Salud Mental y Estrés Académico</h1>
        <p>Aprende a identificar las señales, evalúa tu estado y recupera el control de tu bienestar.</p>
    </header>

    <main>
        <!-- Termómetro de Estrés Interactivo -->
        <section class="widget-box">
            <h2>Termómetro de Estrés Académico</h2>
            <p style="text-align: center; color: #7f8c8d;">Desplaza el selector para reflejar cómo te sientes el día de hoy:</p>
            
            <div class="slider-container">
                <input type="range" min="1" max="10" value="5" class="slider" id="stressSlider">
                <div style="margin-top: 10px; font-size: 1.5rem; font-weight: bold;" id="scoreLabel">Nivel: 5/10</div>
            </div>

            <div id="statusBox" class="status-display">
                Cargando estado...
            </div>
        </section>

        <!-- Bloques de Información Dinámica -->
        <section class="grid">
            <div class="card">
                <h2>⚠️ ¿Cómo se manifiesta?</h2>
                <p>El estrés no solo está en la mente, se divide en tres niveles que debes vigilar:</p>
                <ul style="margin-top: 10px;">
                    <li><strong>Físico:</strong> Dolores de cabeza, tensión en el cuello/hombros, insomnio o fatiga constante.</li>
                    <li><strong>Emocional:</strong> Irritabilidad, ansiedad ante los exámenes, desmotivación o apatía.</li>
                    <li><strong>Conductual:</strong> Procrastinar en exceso, aislamiento social o dificultad para concentrarse.</li>
                </ul>
            </div>

            <div class="card">
                <h2>🛠️ Estrategias de Afrontamiento</h2>
                <p>Abordar el estrés requiere acciones organizadas y directas:</p>
                <ul style="margin-top: 10px;">
                    <li><strong>Planificación Activa:</strong> Desglosa los proyectos grandes en tareas pequeñas de 30 minutos.</li>
                    <li><strong>Técnica Pomodoro:</strong> Estudia 25 minutos sin distracciones y descansa 5 minutos completos.</li>
                    <li><strong>Límites Saludables:</strong> Aprende a decir "no" a responsabilidades extra cuando tu agenda esté saturada.</li>
                </ul>
            </div>
        </section>

        <!-- Herramienta Práctica de Regulación -->
        <section class="card" style="border-top-color: var(--secondary);">
            <h2>🧘 Herramienta de Alivio Inmediato</h2>
            <p>Si sientes que la ansiedad o el agobio por las tareas está subiendo, tómate un minuto para estabilizar tu ritmo cardíaco con este ejercicio guiado.</p>
            <button class="technique-btn" id="startBreatheBtn">Iniciar Respiración Guiada (4-4-4)</button>
            
            <div class="exercise-area" id="breathingArea">
                <h3 id="breathingInstruction">Prepárate...</h3>
                <div class="breathing-circle" id="pulseCircle"></div>
            </div>
        </section>
    </main>

    <footer>
        <p>Mente Sana — Diseñado para el bienestar estudiantil. Si te sientes sobrepasado, recuerda que buscar orientación con un profesional o tutor escolar es un acto de valentía.</p>
    </footer>

    <script>
        // --- Lógica del Termómetro de Estrés ---
        const slider = document.getElementById('stressSlider');
        const scoreLabel = document.getElementById('scoreLabel');
        const statusBox = document.getElementById('statusBox');

        const stressLevels = {
            low: {
                text: "Nivel Seguro: Estrés bajo o manejable. Estás en un buen punto para avanzar con tus entregas con calma.",
                bg: "#e8f8f5", color: "#117a65"
            },
            medium: {
                text: "Nivel Moderado: Alerta de sobrecarga. Es momento de revisar prioridades, organizar tus apuntes y pausar redes sociales.",
                bg: "#fef9e7", color: "#b7950b"
            },
            high: {
                text: "Nivel Crónico: Saturación. Tu rendimiento bajará si no paras. Prioriza dormir 7-8 horas y delega o pospone lo que no sea urgente.",
                bg: "#fdedec", color: "#943126"
            }
        };

        function updateStressView(value) {
            scoreLabel.textContent = `Nivel: ${value}/10`;
            let current;
            if (value <= 3) current = stressLevels.low;
            else if (value <= 7) current = stressLevels.medium;
            else current = stressLevels.high;

            statusBox.textContent = current.text;
            statusBox.style.backgroundColor = current.bg;
            statusBox.style.color = current.color;
        }

        slider.addEventListener('input', (e) => updateStressView(e.target.value));
        updateStressView(slider.value); // Inicialización

        // --- Lógica del Ejercicio de Respiración ---
        const startBtn = document.getElementById('startBreatheBtn');
        const breathingArea = document.getElementById('breathingArea');
        const instruction = document.getElementById('breathingInstruction');
        const circle = document.getElementById('pulseCircle');
        let breathingInterval;

        startBtn.addEventListener('click', () => {
            if (breathingInterval) {
                clearInterval(breathingInterval);
                breathingInterval = null;
                startBtn.textContent = "Iniciar Respiración Guiada (4-4-4)";
                breathingArea.style.display = "none";
                circle.classList.remove('expand');
                return;
            }

            startBtn.textContent = "Detener Ejercicio";
            breathingArea.style.display = "block";
            runBreathingCycle();
            breathingInterval = setInterval(runBreathingCycle, 12000);
        });

        function runBreathingCycle() {
            // Inhala (4s)
            instruction.textContent = "Inhala profundamente por la nariz...";
            circle.style.transition = "transform 4s ease-in-out";
            circle.classList.add('expand');
            
            // Retiene (4s)
            setTimeout(() => {
                instruction.textContent = "Mantén el aire...";
            }, 4000);

            // Exhala (4s)
            setTimeout(() => {
                instruction.textContent = "Exhala despacio por la boca...";
                circle.style.transition = "transform 4s ease-in-out";
                circle.classList.remove('expand');
            }, 8000);
        }
    </script>
</body>
</html>

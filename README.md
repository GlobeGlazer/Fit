<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Planificador de Calistenia</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --color-primary: #191919;
            --color-secondary: #FFFFFF;
            --color-accent: #2EAADC;
            --color-accent-light: #5ABCEB;
            --color-grey: #2A2A2A;
            --color-grey-light: #3A3A3A;
            --color-grey-dark: #1F1F1F;
            --color-success: #4CAF50;
            --color-warning: #FF9800;
            --border-radius: 10px;
            --spacing-xs: 5px;
            --spacing-sm: 10px;
            --spacing-md: 15px;
            --spacing-lg: 20px;
            --spacing-xl: 30px;
            --font-size-sm: 14px;
            --font-size-md: 16px;
            --font-size-lg: 18px;
            --font-size-xl: 22px;
            --font-size-xxl: 26px;
            --shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Helvetica', 'Arial', sans-serif;
        }

        body {
            background-color: var(--color-primary);
            color: var(--color-secondary);
            line-height: 1.5;
            padding: 0;
            font-family: 'Helvetica', 'Arial', sans-serif;
            max-width: 100%;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Header */
        .header {
            background-color: var(--color-primary);
            color: var(--color-secondary);
            padding: var(--spacing-xl) var(--spacing-md);
            text-align: center;
            border-bottom: 3px solid var(--color-accent);
            margin-bottom: var(--spacing-xl);
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
        }

        .header h1 {
            font-size: var(--font-size-xxl);
            margin-bottom: var(--spacing-sm);
            color: var(--color-accent);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .header p {
            font-size: var(--font-size-md);
            opacity: 0.9;
        }

        /* Navegación principal */
        .main-nav {
            display: flex;
            justify-content: center;
            gap: var(--spacing-md);
            margin-bottom: var(--spacing-lg);
            flex-wrap: wrap;
            padding: 0 var(--spacing-md);
        }

        .nav-btn {
            background-color: var(--color-grey);
            color: var(--color-secondary);
            border: none;
            padding: var(--spacing-sm) var(--spacing-lg);
            border-radius: var(--border-radius);
            font-size: var(--font-size-md);
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            font-weight: 600;
            border: 2px solid transparent;
            min-width: 160px;
            justify-content: center;
        }

        .nav-btn:hover {
            background-color: var(--color-grey-light);
            transform: translateY(-2px);
        }

        .nav-btn.active {
            background-color: var(--color-accent);
            color: var(--color-primary);
            border-color: var(--color-accent);
        }

        .nav-btn i {
            font-size: var(--font-size-lg);
        }

        /* Páginas */
        .page {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Página de selección de semana */
        .weeks-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: var(--spacing-md);
            margin-top: var(--spacing-lg);
        }

        .week-card {
            background-color: var(--color-grey);
            border-radius: var(--border-radius);
            padding: var(--spacing-lg);
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            border: 2px solid transparent;
            position: relative;
            overflow: hidden;
        }

        .week-card:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow);
            border-color: var(--color-accent-light);
        }

        .week-card.active {
            border-color: var(--color-accent);
            background-color: var(--color-grey-dark);
        }

        .week-card h3 {
            font-size: var(--font-size-lg);
            margin-bottom: var(--spacing-sm);
            color: var(--color-accent);
        }

        .week-card p {
            font-size: var(--font-size-sm);
            opacity: 0.8;
            margin-bottom: var(--spacing-sm);
        }

        .week-progress {
            height: 5px;
            background-color: var(--color-grey-light);
            border-radius: 10px;
            margin-top: var(--spacing-sm);
            overflow: hidden;
        }

        .week-progress-bar {
            height: 100%;
            background-color: var(--color-success);
            border-radius: 10px;
            width: 0%;
            transition: width 0.5s ease;
        }

        /* Página de selección de día */
        .days-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: var(--spacing-md);
            margin-top: var(--spacing-lg);
        }

        .day-card {
            background-color: var(--color-grey);
            border-radius: var(--border-radius);
            padding: var(--spacing-lg);
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            border: 2px solid transparent;
        }

        .day-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow);
            border-color: var(--color-accent-light);
        }

        .day-card.active {
            border-color: var(--color-accent);
            background-color: var(--color-grey-dark);
        }

        .day-card h3 {
            font-size: var(--font-size-lg);
            margin-bottom: var(--spacing-sm);
            color: var(--color-accent);
        }

        .day-card p {
            font-size: var(--font-size-sm);
            opacity: 0.8;
            margin-bottom: var(--spacing-sm);
        }

        .day-icon {
            font-size: var(--font-size-xl);
            margin-bottom: var(--spacing-sm);
            color: var(--color-accent);
        }

        /* Página de ejercicios */
        .day-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: var(--spacing-lg);
            padding-bottom: var(--spacing-md);
            border-bottom: 2px solid var(--color-grey-light);
            flex-wrap: wrap;
            gap: var(--spacing-md);
        }

        .day-title {
            font-size: var(--font-size-xl);
            color: var(--color-accent);
        }

        .day-progress {
            background-color: var(--color-grey);
            padding: var(--spacing-sm) var(--spacing-lg);
            border-radius: var(--border-radius);
            font-size: var(--font-size-md);
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
        }

        .day-progress-bar {
            height: 8px;
            width: 150px;
            background-color: var(--color-grey-light);
            border-radius: 10px;
            overflow: hidden;
        }

        .day-progress-fill {
            height: 100%;
            background-color: var(--color-accent);
            border-radius: 10px;
            width: 0%;
            transition: width 0.5s ease;
        }

        .exercises-list {
            margin-top: var(--spacing-lg);
        }

        .exercise-card {
            background-color: var(--color-grey);
            border-radius: var(--border-radius);
            padding: var(--spacing-lg);
            margin-bottom: var(--spacing-md);
            border-left: 4px solid var(--color-accent);
            position: relative;
            transition: var(--transition);
        }

        .exercise-card:hover {
            background-color: var(--color-grey-dark);
        }

        .exercise-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: var(--spacing-md);
            flex-wrap: wrap;
            gap: var(--spacing-sm);
        }

        .exercise-name {
            font-size: var(--font-size-lg);
            font-weight: 600;
            color: var(--color-secondary);
            flex: 1;
        }

        .exercise-info-btn {
            background-color: var(--color-accent);
            color: var(--color-primary);
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
            font-weight: bold;
        }

        .exercise-info-btn:hover {
            background-color: var(--color-accent-light);
            transform: scale(1.1);
        }

        .exercise-details {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: var(--spacing-md);
            flex-wrap: wrap;
            gap: var(--spacing-md);
        }

        .exercise-sets {
            background-color: var(--color-grey-dark);
            padding: var(--spacing-sm) var(--spacing-md);
            border-radius: var(--border-radius);
            font-size: var(--font-size-md);
            font-weight: 600;
            color: var(--color-accent);
        }

        .exercise-muscles {
            font-size: var(--font-size-sm);
            background-color: var(--color-grey-light);
            padding: var(--spacing-xs) var(--spacing-md);
            border-radius: var(--border-radius);
            color: var(--color-secondary);
            opacity: 0.9;
        }

        .sets-container {
            display: flex;
            gap: var(--spacing-md);
            margin-top: var(--spacing-md);
            flex-wrap: wrap;
        }

        .set-btn {
            background-color: var(--color-grey-dark);
            color: var(--color-secondary);
            border: 2px solid var(--color-grey-light);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: var(--font-size-md);
            transition: var(--transition);
            flex-shrink: 0;
        }

        .set-btn:hover {
            border-color: var(--color-accent);
        }

        .set-btn.completed {
            background-color: var(--color-success);
            color: var(--color-primary);
            border-color: var(--color-success);
        }

        /* Modal de información del ejercicio */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: var(--spacing-md);
            display: none;
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal {
            background-color: var(--color-grey);
            border-radius: var(--border-radius);
            width: 100%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
            border: 2px solid var(--color-accent);
            position: relative;
            animation: modalFadeIn 0.3s ease;
        }

        @keyframes modalFadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .modal-header {
            background-color: var(--color-accent);
            color: var(--color-primary);
            padding: var(--spacing-lg);
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-header h3 {
            font-size: var(--font-size-xl);
            font-weight: 700;
        }

        .modal-close {
            background: none;
            border: none;
            color: var(--color-primary);
            font-size: var(--font-size-xl);
            cursor: pointer;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            transition: var(--transition);
        }

        .modal-close:hover {
            background-color: rgba(0, 0, 0, 0.1);
        }

        .modal-body {
            padding: var(--spacing-lg);
        }

        .modal-section {
            margin-bottom: var(--spacing-lg);
        }

        .modal-section h4 {
            color: var(--color-accent);
            font-size: var(--font-size-lg);
            margin-bottom: var(--spacing-sm);
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
        }

        .modal-section p {
            font-size: var(--font-size-md);
            line-height: 1.6;
        }

        .modal-section ul {
            padding-left: var(--spacing-lg);
            font-size: var(--font-size-md);
            line-height: 1.6;
        }

        .modal-section li {
            margin-bottom: var(--spacing-xs);
        }

        /* Botones de navegación */
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: var(--spacing-xl);
            flex-wrap: wrap;
            gap: var(--spacing-md);
        }

        .btn {
            background-color: var(--color-accent);
            color: var(--color-primary);
            border: none;
            padding: var(--spacing-md) var(--spacing-xl);
            border-radius: var(--border-radius);
            font-size: var(--font-size-md);
            cursor: pointer;
            transition: var(--transition);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            flex: 1;
            justify-content: center;
            min-width: 140px;
        }

        .btn:hover {
            background-color: var(--color-accent-light);
            transform: translateY(-2px);
            box-shadow: var(--shadow);
        }

        .btn-secondary {
            background-color: var(--color-grey);
            color: var(--color-secondary);
        }

        .btn-secondary:hover {
            background-color: var(--color-grey-light);
        }

        /* Pie de página */
        .footer {
            text-align: center;
            padding: var(--spacing-lg);
            margin-top: var(--spacing-xl);
            font-size: var(--font-size-sm);
            opacity: 0.7;
            border-top: 1px solid var(--color-grey-light);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .weeks-grid, .days-grid {
                grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
            }
            
            .nav-btn {
                padding: var(--spacing-sm) var(--spacing-md);
                font-size: var(--font-size-sm);
            }
            
            .day-header {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .day-progress {
                width: 100%;
            }
            
            .exercise-header {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .exercise-info-btn {
                position: absolute;
                top: var(--spacing-lg);
                right: var(--spacing-lg);
            }
        }

        @media (max-width: 480px) {
            .weeks-grid, .days-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .header h1 {
                font-size: var(--font-size-lg);
            }
            
            .btn {
                min-width: 100%;
            }
        }

        /* Utilitarios */
        .hidden {
            display: none !important;
        }

        .text-center {
            text-align: center;
        }

        .mt-1 { margin-top: var(--spacing-sm); }
        .mt-2 { margin-top: var(--spacing-md); }
        .mt-3 { margin-top: var(--spacing-lg); }
        .mt-4 { margin-top: var(--spacing-xl); }

        .mb-1 { margin-bottom: var(--spacing-sm); }
        .mb-2 { margin-bottom: var(--spacing-md); }
        .mb-3 { margin-bottom: var(--spacing-lg); }
        .mb-4 { margin-bottom: var(--spacing-xl); }
        
        .loading {
            text-align: center;
            padding: var(--spacing-xl);
            color: var(--color-accent);
        }
        
        .loading i {
            font-size: var(--font-size-xxl);
            margin-bottom: var(--spacing-md);
        }
    </style>
</head>
<body>
    <div class="header">
        <h1><i class="fas fa-dumbbell"></i> PLANIFICADOR DE CALISTENIA</h1>
        <p>Sigue tu progreso y domina cada ejercicio</p>
    </div>

    <div class="container">
        <!-- Navegación principal -->
        <div class="main-nav">
            <button class="nav-btn active" id="btn-weeks">
                <i class="fas fa-calendar-alt"></i> Semanas
            </button>
            <button class="nav-btn" id="btn-days">
                <i class="fas fa-calendar-day"></i> Días
            </button>
            <button class="nav-btn" id="btn-exercises">
                <i class="fas fa-running"></i> Ejercicios
            </button>
        </div>

        <!-- Página de semanas -->
        <div class="page active" id="page-weeks">
            <h2 class="text-center">Selecciona una semana de entrenamiento</h2>
            <p class="text-center mt-1 mb-3">Tu plan tiene 52 semanas de entrenamiento progresivo</p>
            <div class="weeks-grid" id="weeks-container">
                <!-- Las semanas se generarán dinámicamente con JavaScript -->
            </div>
        </div>

        <!-- Página de días -->
        <div class="page" id="page-days">
            <h2 class="text-center">Selecciona un día de entrenamiento</h2>
            <p class="text-center mt-1 mb-3" id="current-week-title">Semana 1: Técnica, Control & Base Avanzada</p>
            <div class="days-grid" id="days-container">
                <!-- Los días se generarán dinámicamente con JavaScript -->
            </div>
            <div class="nav-buttons">
                <button class="btn btn-secondary" id="btn-back-to-weeks">
                    <i class="fas fa-arrow-left"></i> Volver a semanas
                </button>
            </div>
        </div>

        <!-- Página de ejercicios -->
        <div class="page" id="page-exercises">
            <div class="day-header">
                <div>
                    <h2 class="day-title" id="day-title">Lunes (Push)</h2>
                    <p id="week-subtitle">Semana 1: Técnica, Control & Base Avanzada</p>
                </div>
                <div class="day-progress">
                    <span id="progress-text">0% completado</span>
                    <div class="day-progress-bar">
                        <div class="day-progress-fill" id="day-progress-fill"></div>
                    </div>
                </div>
            </div>

            <div class="exercises-list" id="exercises-container">
                <!-- Los ejercicios se generarán dinámicamente con JavaScript -->
            </div>

            <div class="nav-buttons">
                <button class="btn btn-secondary" id="btn-back-to-days">
                    <i class="fas fa-arrow-left"></i> Volver a días
                </button>
                <button class="btn" id="btn-reset-day">
                    <i class="fas fa-redo"></i> Reiniciar día
                </button>
            </div>
        </div>
    </div>

    <!-- Modal de información del ejercicio -->
    <div class="modal-overlay" id="exercise-modal">
        <div class="modal">
            <div class="modal-header">
                <h3 id="modal-exercise-name">Nombre del ejercicio</h3>
                <button class="modal-close" id="modal-close-btn">&times;</button>
            </div>
            <div class="modal-body">
                <div class="modal-section">
                    <h4><i class="fas fa-info-circle"></i> Descripción</h4>
                    <p id="modal-description">Descripción del ejercicio...</p>
                </div>
                <div class="modal-section">
                    <h4><i class="fas fa-dumbbell"></i> Músculos trabajados</h4>
                    <ul id="modal-muscles">
                        <!-- Los músculos se añadirán dinámicamente -->
                    </ul>
                </div>
                <div class="modal-section">
                    <h4><i class="fas fa-clipboard-check"></i> Recomendaciones</h4>
                    <ul id="modal-recommendations">
                        <!-- Las recomendaciones se añadirán dinámicamente -->
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <div class="footer">
        <p>Planificador de Calistenia &copy; 2023 | Diseñado para entrenamiento funcional</p>
        <p class="mt-1">Tu progreso se guarda automáticamente en tu dispositivo</p>
    </div>

    <script>
        // Datos del plan de entrenamiento - EXTRAÍDOS DIRECTAMENTE DEL DOCUMENTO
        const trainingPlan = {
            weeks: [
                // SEMANA 1
                {
                    id: 1,
                    title: "Técnica, Control & Base Avanzada",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Push-ups con pausa al fondo", sets: 3, reps: "12", type: "push" },
                                { name: "Declined push-ups", sets: 3, reps: "10", type: "push" },
                                { name: "Diamond push-ups lentos", sets: 3, reps: "8", type: "push" },
                                { name: "Archer push-ups", sets: 3, reps: "6 por lado", type: "push" },
                                { name: "Core finisher: Hollow Hold + V-ups + Leg Raises (circuito)", sets: 1, reps: "10 min", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio (30 min suave)", sets: 1, reps: "30 min", type: "cardio" },
                                { name: "Flexibilidad (mínimo 20 minutos)", sets: 1, reps: "20 min", type: "flex" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Pull-ups strict", sets: 3, reps: "max", type: "pull" },
                                { name: "Chin-ups", sets: 3, reps: "10", type: "pull" },
                                { name: "Australian rows con pausa", sets: 3, reps: "12", type: "pull" },
                                { name: "Superman hold 3x30\" + scapular shrugs colgado", sets: 3, reps: "30\" + 10", type: "pull" },
                                { name: "Core finisher: Hanging knee raises", sets: 3, reps: "15", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Bulgarian split squats", sets: 3, reps: "10 por pierna", type: "legs" },
                                { name: "Explosive jump squats", sets: 4, reps: "8", type: "legs" },
                                { name: "Lateral squats", sets: 3, reps: "10", type: "legs" },
                                { name: "Calf raises + isométrico 2 segundos", sets: 4, reps: "15", type: "legs" },
                                { name: "Core finisher: Side plank to crunch", sets: 3, reps: "12 por lado", type: "core" }
                            ]
                        }
                    }
                },
                // SEMANA 2 y 3
                {
                    id: 2,
                    title: "Endurance, Variation & Core Strength",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Explosive push-ups", sets: 3, reps: "8", type: "push" },
                                { name: "Pseudo planche push-ups", sets: 3, reps: "10", type: "push" },
                                { name: "Inclined archer push-ups", sets: 3, reps: "6 por lado", type: "push" },
                                { name: "Dips en silla", sets: 3, reps: "12 lentos", type: "push" },
                                { name: "Core finisher: 3 rondas (15 mountain climbers + 10 hollow rocks + 30\" plank hold)", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio (30 min suave)", sets: 1, reps: "30 min", type: "cardio" },
                                { name: "Flexibilidad (mínimo 20 minutos)", sets: 1, reps: "20 min", type: "flex" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Pull-ups con tempo 2-1-2", sets: 3, reps: "max", type: "pull" },
                                { name: "Australian rows con pies elevados", sets: 4, reps: "10", type: "pull" },
                                { name: "Chin-ups con pausa arriba", sets: 3, reps: "8", type: "pull" },
                                { name: "Scapular pull-ups", sets: 3, reps: "12", type: "pull" },
                                { name: "Core finisher: 3x20 Russian twists + 15 leg raises + 30\" hollow hold", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Bulgarian split squats", sets: 3, reps: "10 por pierna", type: "legs" },
                                { name: "Explosive jump squats", sets: 4, reps: "8", type: "legs" },
                                { name: "Lateral squats", sets: 3, reps: "10", type: "legs" },
                                { name: "Calf raises + isométrico 2 segundos", sets: 4, reps: "15", type: "legs" },
                                { name: "Core finisher: Side plank to crunch", sets: 3, reps: "12 por lado", type: "core" }
                            ]
                        }
                    }
                },
                // SEMANA 3
                {
                    id: 3,
                    title: "Endurance, Variation & Core Strength",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Explosive push-ups", sets: 3, reps: "8", type: "push" },
                                { name: "Pseudo planche push-ups", sets: 3, reps: "10", type: "push" },
                                { name: "Inclined archer push-ups", sets: 3, reps: "6 por lado", type: "push" },
                                { name: "Dips en silla", sets: 3, reps: "12 lentos", type: "push" },
                                { name: "Core finisher: 3 rondas (15 mountain climbers + 10 hollow rocks + 30\" plank hold)", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio (30 min suave)", sets: 1, reps: "30 min", type: "cardio" },
                                { name: "Flexibilidad (mínimo 20 minutos)", sets: 1, reps: "20 min", type: "flex" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Pull-ups con tempo 2-1-2", sets: 3, reps: "max", type: "pull" },
                                { name: "Australian rows con pies elevados", sets: 4, reps: "10", type: "pull" },
                                { name: "Chin-ups con pausa arriba", sets: 3, reps: "8", type: "pull" },
                                { name: "Scapular pull-ups", sets: 3, reps: "12", type: "pull" },
                                { name: "Core finisher: 3x20 Russian twists + 15 leg raises + 30\" hollow hold", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Bulgarian split squats", sets: 3, reps: "10 por pierna", type: "legs" },
                                { name: "Explosive jump squats", sets: 4, reps: "8", type: "legs" },
                                { name: "Lateral squats", sets: 3, reps: "10", type: "legs" },
                                { name: "Calf raises + isométrico 2 segundos", sets: 4, reps: "15", type: "legs" },
                                { name: "Core finisher: Side plank to crunch", sets: 3, reps: "12 por lado", type: "core" }
                            ]
                        }
                    }
                },
                // SEMANA 4 y 5
                {
                    id: 4,
                    title: "Controlled Tension & New Transitions",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Push-ups con tempo 3-1-1", sets: 3, reps: "10", type: "push" },
                                { name: "Pike push-ups (hombros)", sets: 3, reps: "8", type: "push" },
                                { name: "Pseudo planche push-ups", sets: 3, reps: "12", type: "push" },
                                { name: "Explosive push-ups + pausa abajo", sets: 3, reps: "6", type: "push" },
                                { name: "Core finisher: 3 rondas (10 slow V-ups + 20 mountain climbers + 30\" plank)", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio: 25–30 min trote/cuerda/bici suave", sets: 1, reps: "25-30 min", type: "cardio" },
                                { name: "Flexibilidad guiada (25 min)", sets: 1, reps: "25 min", type: "flex" },
                                { name: "Respiración 4-7-8 + 5 min sentado en silencio", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Archer pull-ups", sets: 3, reps: "6 por lado", type: "pull" },
                                { name: "Inverted rows lentos con pies elevados", sets: 4, reps: "8", type: "pull" },
                                { name: "Chin-ups con lastre liviano o mochila", sets: 3, reps: "6–8", type: "pull" },
                                { name: "Scapular holds colgado", sets: 3, reps: "20 seg", type: "pull" },
                                { name: "Core finisher: 3x15 hanging leg raises + 30\" hollow hold", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Wall sit isométrico 60s con peso (mochila)", sets: 3, reps: "60s", type: "legs" },
                                { name: "Skater squats asistidos", sets: 3, reps: "6 por pierna", type: "legs" },
                                { name: "Jump lunges (explosión vertical)", sets: 3, reps: "8", type: "legs" },
                                { name: "Elevated calf raises (con pausa arriba)", sets: 4, reps: "15", type: "legs" },
                                { name: "Core finisher: 3x20 toe touches + 30\" plancha con elevación alternada de pie", sets: 3, reps: "circuito", type: "core" }
                            ]
                        }
                    }
                },
                // SEMANA 5
                {
                    id: 5,
                    title: "Controlled Tension & New Transitions",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Push-ups con tempo 3-1-1", sets: 3, reps: "10", type: "push" },
                                { name: "Pike push-ups (hombros)", sets: 3, reps: "8", type: "push" },
                                { name: "Pseudo planche push-ups", sets: 3, reps: "12", type: "push" },
                                { name: "Explosive push-ups + pausa abajo", sets: 3, reps: "6", type: "push" },
                                { name: "Core finisher: 3 rondas (10 slow V-ups + 20 mountain climbers + 30\" plank)", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio: 25–30 min trote/cuerda/bici suave", sets: 1, reps: "25-30 min", type: "cardio" },
                                { name: "Flexibilidad guiada (25 min)", sets: 1, reps: "25 min", type: "flex" },
                                { name: "Respiración 4-7-8 + 5 min sentado en silencio", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Archer pull-ups", sets: 3, reps: "6 por lado", type: "pull" },
                                { name: "Inverted rows lentos con pies elevados", sets: 4, reps: "8", type: "pull" },
                                { name: "Chin-ups con lastre liviano o mochila", sets: 3, reps: "6–8", type: "pull" },
                                { name: "Scapular holds colgado", sets: 3, reps: "20 seg", type: "pull" },
                                { name: "Core finisher: 3x15 hanging leg raises + 30\" hollow hold", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Wall sit isométrico 60s con peso (mochila)", sets: 3, reps: "60s", type: "legs" },
                                { name: "Skater squats asistidos", sets: 3, reps: "6 por pierna", type: "legs" },
                                { name: "Jump lunges (explosión vertical)", sets: 3, reps: "8", type: "legs" },
                                { name: "Elevated calf raises (con pausa arriba)", sets: 4, reps: "15", type: "legs" },
                                { name: "Core finisher: 3x20 toe touches + 30\" plancha con elevación alternada de pie", sets: 3, reps: "circuito", type: "core" }
                            ]
                        }
                    }
                },
                // SEMANA 6
                {
                    id: 6,
                    title: "Technical Mastery & Complete Endurance",
                    days: {
                        lunes: {
                            title: "Lunes (Push)",
                            exercises: [
                                { name: "Pseudo planche push-ups con pausa", sets: 3, reps: "10", type: "push" },
                                { name: "Pike push-ups en bloque lento (3-1-3 tempo)", sets: 3, reps: "8", type: "push" },
                                { name: "Elevated feet push-ups + explosión", sets: 3, reps: "10", type: "push" },
                                { name: "Diamond push-ups hasta fallo técnico", sets: 2, reps: "max", type: "push" },
                                { name: "Core finisher: 3 rondas (15 flutter kicks + 10 leg raises + 20\" plank shoulder taps)", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        martes: {
                            title: "Martes (Flexy)",
                            exercises: [
                                { name: "Cardio (opcional): caminata o trote suave 30 min", sets: 1, reps: "30 min", type: "cardio" },
                                { name: "Flexibilidad total (30 min)", sets: 1, reps: "30 min", type: "flex" },
                                { name: "Técnica de respiración: 2 rondas de respiración box o método Wim Hof básico", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        miercoles: {
                            title: "Miércoles (Pull)",
                            exercises: [
                                { name: "Pull-ups tempo 3-1-3", sets: 3, reps: "6–8", type: "pull" },
                                { name: "Negative pull-ups (descenso lento 5 seg)", sets: 3, reps: "5", type: "pull" },
                                { name: "Body rows + hollow body hold 2 seg arriba", sets: 4, reps: "8", type: "pull" },
                                { name: "Scapular pull-ups + hangs", sets: 3, reps: "15", type: "pull" },
                                { name: "Core finisher: 3x20 Russian twists + 3x15 hanging knee raises", sets: 3, reps: "circuito", type: "core" }
                            ]
                        },
                        jueves: {
                            title: "Jueves (Push/Pull)",
                            exercises: [
                                { name: "Repetir día débil (Push/Pull/Legs)", sets: 1, reps: "Personalizado", type: "mixed" },
                                { name: "Caminar 45 min", sets: 1, reps: "45 min", type: "cardio" },
                                { name: "Yoga o estiramiento largo", sets: 1, reps: "Personalizado", type: "flex" },
                                { name: "Automasaje con pelota o foam roller", sets: 1, reps: "Personalizado", type: "recovery" }
                            ]
                        },
                        viernes: {
                            title: "Viernes (Leg)",
                            exercises: [
                                { name: "Bulgarian split squat con pausa abajo", sets: 3, reps: "8", type: "legs" },
                                { name: "Wall sit 60s + immediately 15 jump squats", sets: 3, reps: "circuito", type: "legs" },
                                { name: "Step-ups con mochila", sets: 3, reps: "10 por pierna", type: "legs" },
                                { name: "Lateral lunges con apoyo mínimo", sets: 3, reps: "10", type: "legs" },
                                { name: "Core finisher: 3x20 bicycle crunch + 3x20\" side plank holds", sets: 3, reps: "circuito", type: "core" }
                            ]
                        }
                    }
                }
            ]
        };

        // Completar con semanas genéricas hasta la 52 para demostración
        for (let i = 7; i <= 52; i++) {
            let title = "";
            if (i === 7) title = "Technical Mastery & Complete Endurance";
            else if (i >= 8 && i <= 9) title = "Advanced Resistance & Mind Control";
            else if (i >= 10 && i <= 11) title = "Athletic Control & Coordinated Tension";
            else if (i >= 12 && i <= 13) title = "Functional Power & Control in Movement";
            else if (i >= 14 && i <= 15) title = "Maximum Tension + Body Control Assessment";
            else if (i >= 16 && i <= 17) title = "Density, Technical Volume and Breathing Under Tension";
            else if (i >= 18 && i <= 20) title = "Fatigue Accuracy & Body Unity";
            else if (i === 21) title = "Dynamic Stability & Athletic Technical Control";
            else if (i >= 22 && i <= 23) title = "Technical Consolidation & Overall Performance";
            else if (i >= 24 && i <= 25) title = "Athletic Fluidity & Continuous Power";
            else if (i >= 26 && i <= 27) title = "Athletic Endurance & Controlled Agility";
            else if (i >= 28 && i <= 29) title = "Advanced Athletic Strength & Fluid Transitions";
            else if (i >= 30 && i <= 31) title = "Maximum Strength with Structural Control and Balance";
            else if (i >= 32 && i <= 33) title = "Controlled Explosiveness & Advanced Body Awareness";
            else if (i >= 34 && i <= 36) title = "Technical Mastery & Comprehensive Athletic Body";
            else if (i === 37) title = "Power Under Fatigue & Body as a Unit";
            else if (i >= 38 && i <= 39) title = "Advanced Technical Endurance & Breathing Under Tension";
            else if (i >= 40 && i <= 41) title = "Postural Precision & Explosiveness without Collapse";
            else if (i >= 42 && i <= 43) title = "True Athletic Power & Internal Tension Mastery";
            else if (i >= 44 && i <= 45) title = "Fluid Body Unit & Efficient Breathing Under Load";
            else if (i >= 46 && i <= 47) title = "Absolute Integration of Strength, Breathing & Posture";
            else if (i >= 48 && i <= 49) title = "Technical Consolidation & Presence in Motion";
            else if (i >= 50 && i <= 51) title = "Total Integration, Physical Gratitude and Effortless Control";
            else title = "Consolidación final";
            
            trainingPlan.weeks.push({
                id: i,
                title: title,
                days: JSON.parse(JSON.stringify(trainingPlan.weeks[5].days))
            });
        }

        // Información detallada de TODOS los ejercicios del documento
        const exerciseInfo = {
            "Push-ups con pausa al fondo": {
                description: "Flexiones con pausa de 2-3 segundos en la posición más baja para mayor activación muscular.",
                muscles: ["Pectoral mayor", "Tríceps", "Deltoides anterior", "Core"],
                recommendations: [
                    "Mantén el cuerpo en línea recta",
                    "Baja lentamente en 3 segundos",
                    "Pausa completa en la parte inferior",
                    "Sube con control"
                ]
            },
            "Declined push-ups": {
                description: "Flexiones con pies elevados para mayor intensidad y enfoque en pectoral superior.",
                muscles: ["Pectoral superior", "Tríceps", "Deltoides anterior", "Core"],
                recommendations: [
                    "Eleva pies sobre banco o superficie estable",
                    "Mantén manos ligeramente más anchas que hombros",
                    "Controla el descenso completo",
                    "Mantén codos a 45°"
                ]
            },
            "Diamond push-ups lentos": {
                description: "Flexiones con manos en forma de diamante para enfatizar tríceps.",
                muscles: ["Tríceps", "Pectoral interno", "Deltoides anterior"],
                recommendations: [
                    "Manos juntas formando diamante bajo pecho",
                    "Codos pegados al cuerpo",
                    "Ejecución lenta: 3s bajar, 1s pausa, 2s subir",
                    "Mantén core activado"
                ]
            },
            "Archer push-ups": {
                description: "Flexiones asimétricas que preparan para planche push-ups.",
                muscles: ["Pectoral", "Tríceps", "Deltoides", "Core estabilizador"],
                recommendations: [
                    "Manos más anchas que hombros",
                    "Desplaza peso hacia un lado al bajar",
                    "Brazo contrario extendido pero relajado",
                    "Alterna lados equitativamente"
                ]
            },
            "Explosive push-ups": {
                description: "Flexiones con fase concéntrica explosiva para desarrollar potencia.",
                muscles: ["Pectoral", "Tríceps", "Deltoides anterior", "Core"],
                recommendations: [
                    "Baja con control",
                    "Empuja explosivamente hacia arriba",
                    "Mantén core tenso durante el impulso",
                    "Aterriza suavemente"
                ]
            },
            "Pseudo planche push-ups": {
                description: "Flexiones con manos cerca de la cadera, simulando posición de plancha.",
                muscles: ["Pectoral inferior", "Deltoides anterior", "Tríceps", "Core"],
                recommendations: [
                    "Manos a la altura de las caderas",
                    "Inclina torso hacia adelante",
                    "Mantén codos pegados al cuerpo",
                    "Progresión gradual: comienza inclinado"
                ]
            },
            "Pike push-ups": {
                description: "Flexiones en posición de pica para enfocar hombros.",
                muscles: ["Deltoides anterior y medio", "Tríceps", "Trapecio superior", "Core"],
                recommendations: [
                    "Cadera alta formando ángulo de 90°",
                    "Baja cabeza hacia el suelo entre manos",
                    "Mantén piernas rectas",
                    "Para mayor dificultad: eleva pies"
                ]
            },
            "Push-ups con tempo 3-1-1": {
                description: "Flexiones con tempo controlado: 3 segundos bajando, 1 segundo pausa, 1 segundo subiendo.",
                muscles: ["Pectoral", "Tríceps", "Deltoides anterior", "Core"],
                recommendations: [
                    "Controla el descenso contando 3 segundos",
                    "Pausa completa en la parte inferior",
                    "Sube en 1 segundo manteniendo control",
                    "Respira profundamente durante la pausa"
                ]
            },
            "Pull-ups strict": {
                description: "Dominadas estrictas sin balanceo ni impulso.",
                muscles: ["Dorsal ancho", "Trapecio", "Bíceps", "Romboides"],
                recommendations: [
                    "Agarre prono (palmas hacia adelante)",
                    "Comienza desde posición colgado completamente",
                    "Sube hasta barbilla sobre la barra",
                    "Evita balancear las piernas"
                ]
            },
            "Chin-ups": {
                description: "Dominadas con agarre supino para mayor participación del bíceps.",
                muscles: ["Bíceps", "Dorsal ancho", "Trapecio inferior"],
                recommendations: [
                    "Agarre supino (palmas hacia ti)",
                    "Anchura de hombros",
                    "Concéntrate en acercar el pecho a la barra",
                    "Controla el descenso"
                ]
            },
            "Australian rows con pausa": {
                description: "Remo invertido con pausa en la contracción máxima.",
                muscles: ["Dorsal medio", "Trapecio", "Romboides", "Bíceps"],
                recommendations: [
                    "Cuerpo recto de talones a cabeza",
                    "Junta omóplatos al subir",
                    "Pausa de 2 segundos en la parte superior",
                    "Baja con control completo"
                ]
            },
            "Superman hold 3x30\" + scapular shrugs colgado": {
                description: "Combinación de superman estático y encogimiento de hombros colgado.",
                muscles: ["Erector espinal", "Trapecio", "Romboides", "Glúteos"],
                recommendations: [
                    "Superman: eleva brazos y piernas manteniendo cuello neutral",
                    "Scapular shrugs: eleva hombros hacia las orejas",
                    "Mantén contracciones durante el tiempo indicado",
                    "Respira profundamente"
                ]
            },
            "Bulgarian split squats": {
                description: "Sentadilla unilateral con pierna trasera elevada.",
                muscles: ["Cuádriceps", "Glúteos", "Isquiotibiales", "Pantorrillas"],
                recommendations: [
                    "Mantén torso erguido",
                    "Baja hasta muslo paralelo al suelo",
                    "Rodilla no debe pasar la punta del pie",
                    "Alterna piernas para equilibrio"
                ]
            },
            "Explosive jump squats": {
                description: "Sentadillas con salto explosivo para potencia.",
                muscles: ["Cuádriceps", "Glúteos", "Pantorrillas", "Core"],
                recommendations: [
                    "Baja en sentadilla controlada",
                    "Explota hacia arriba con máxima fuerza",
                    "Aterriza suavemente doblando rodillas",
                    "Mantén pecho alto"
                ]
            },
            "Lateral squats": {
                description: "Sentadillas laterales para trabajo de aductores y glúteo medio.",
                muscles: ["Aductores", "Glúteo medio", "Cuádriceps", "Isquiotibiales"],
                recommendations: [
                    "Paso lateral amplio",
                    "Mantén pierna de apoyo recta",
                    "Baja controladamente",
                    "Vuelve a posición inicial empujando con el talón"
                ]
            },
            "Calf raises + isométrico 2 segundos": {
                description: "Elevaciones de talón con pausa en la contracción máxima.",
                muscles: ["Gastrocnemio", "Sóleo", "Tibial posterior"],
                recommendations: [
                    "Eleva talones lo más alto posible",
                    "Mantén contracción máxima 2 segundos",
                    "Baja lentamente con control",
                    "Para intensidad: una pierna"
                ]
            },
            "Side plank to crunch": {
                description: "Combinación de plancha lateral y crunch para oblicuos.",
                muscles: ["Oblicuos", "Transverso abdominal", "Glúteo medio"],
                recommendations: [
                    "Mantén línea recta en plancha lateral",
                    "Al hacer crunch, acerca codo y rodilla",
                    "Controla movimiento en ambas direcciones",
                    "Respira exhalando durante el crunch"
                ]
            },
            "Cardio (30 min suave)": {
                description: "Cardio de baja intensidad para resistencia y recuperación.",
                muscles: ["Sistema cardiovascular", "Piernas"],
                recommendations: [
                    "Mantén ritmo que permita hablar cómodamente",
                    "Varía actividades para evitar aburrimiento",
                    "Hidrátate adecuadamente",
                    "Respira nasalmente si es posible"
                ]
            },
            "Flexibilidad (mínimo 20 minutos)": {
                description: "Sesión de estiramientos para movilidad y prevención de lesiones.",
                muscles: ["Cadena posterior completa", "Flexores de cadera", "Espalda"],
                recommendations: [
                    "Calienta ligeramente antes",
                    "Mantén estiramientos 20-30 segundos",
                    "No rebotes, mantén tensión constante",
                    "Respira profundamente"
                ]
            },
            "Repetir día débil (Push/Pull/Legs)": {
                description: "Sesión para trabajar grupos musculares que necesitan más desarrollo.",
                muscles: ["Varía según selección"],
                recommendations: [
                    "Identifica tus puntos débiles",
                    "Enfócate en técnica perfecta",
                    "Usa ejercicios de aislamiento",
                    "Registra tu progreso"
                ]
            },
            "Caminar 45 min": {
                description: "Caminata a ritmo moderado para recuperación activa.",
                muscles: ["Cuádriceps", "Glúteos", "Pantorrillas", "Sistema cardiovascular"],
                recommendations: [
                    "Ritmo constante que eleve ligeramente frecuencia cardíaca",
                    "Preferiblemente al aire libre",
                    "Usa calzado adecuado",
                    "Aprovecha para desconectar mentalmente"
                ]
            },
            "Yoga o estiramiento largo": {
                description: "Sesión prolongada de yoga o estiramientos profundos.",
                muscles: ["Todos los grupos musculares"],
                recommendations: [
                    "Dedica 30-45 minutos mínimo",
                    "Enfócate en áreas tensas",
                    "Usa respiración para profundizar",
                    "Mantén cada postura 30+ segundos"
                ]
            },
            "Automasaje con pelota o foam roller": {
                description: "Liberación miofascial para aliviar tensión muscular.",
                muscles: ["Puntos gatillo varios"],
                recommendations: [
                    "Enfócate en áreas con tensión",
                    "Aplica presión sostenida 30-60 segundos",
                    "Respira profundamente durante la presión",
                    "Evita huesos y articulaciones"
                ]
            },
            "Core finisher: Hollow Hold + V-ups + Leg Raises": {
                description: "Circuito de ejercicios avanzados para core.",
                muscles: ["Recto abdominal", "Oblicuos", "Transverso", "Flexores cadera"],
                recommendations: [
                    "Hollow hold: espalda baja pegada al suelo",
                    "V-ups: controla movimiento, sin impulso",
                    "Leg raises: baja piernas lentamente",
                    "Descansa 30s entre ejercicios"
                ]
            },
            "Dips en silla": {
                description: "Fondos en silla para tríceps y pecho.",
                muscles: ["Tríceps", "Pectoral inferior", "Deltoides anterior"],
                recommendations: [
                    "Manos en silla, pies en suelo",
                    "Baja hasta codos a 90°",
                    "Mantén codos hacia atrás",
                    "No bloquees codos al subir"
                ]
            },
            "Inclined archer push-ups": {
                description: "Archer push-ups en superficie inclinada para progresión.",
                muscles: ["Pectoral", "Tríceps", "Deltoides", "Core"],
                recommendations: [
                    "Usa superficie inclinada para reducir intensidad",
                    "Mantén técnica igual que archer normal",
                    "Progresiona a superficie horizontal",
                    "Alterna lados equitativamente"
                ]
            },
            "Pull-ups con tempo 2-1-2": {
                description: "Dominadas con tempo controlado específico.",
                muscles: ["Dorsal ancho", "Bíceps", "Trapecio", "Romboides"],
                recommendations: [
                    "2 segundos subiendo",
                    "1 segundo pausa arriba",
                    "2 segundos bajando",
                    "Mantén control en todo momento"
                ]
            },
            "Australian rows con pies elevados": {
                description: "Remo invertido con mayor dificultad.",
                muscles: ["Dorsal ancho", "Trapecio", "Romboides", "Bíceps"],
                recommendations: [
                    "Eleva pies sobre banco",
                    "Mantén cuerpo recto",
                    "Junta omóplatos al subir",
                    "Baja completamente"
                ]
            },
            "Chin-ups con pausa arriba": {
                description: "Chin-ups con pausa en la contracción máxima.",
                muscles: ["Bíceps", "Dorsal ancho", "Trapecio inferior"],
                recommendations: [
                    "Sube hasta barbilla sobre barra",
                    "Pausa 2 segundos en posición superior",
                    "Mantén contracción máxima",
                    "Baja con control"
                ]
            },
            "Scapular pull-ups": {
                description: "Activación escapular desde posición colgada.",
                muscles: ["Trapecio inferior", "Romboides", "Dorsal"],
                recommendations: [
                    "Comienza colgado con brazos extendidos",
                    "Eleva hombros hacia abajo y atrás",
                    "Mantén brazos rectos",
                    "Siente contracción entre omóplatos"
                ]
            },
            "Wall sit isométrico 60s con peso": {
                description: "Isométrico de sentadilla en pared con peso adicional.",
                muscles: ["Cuádriceps", "Glúteos", "Isquiotibiales"],
                recommendations: [
                    "Espalda contra pared, rodillas 90°",
                    "Mantén posición durante tiempo indicado",
                    "Añade peso con mochila si es posible",
                    "Respira profundamente durante la contracción"
                ]
            },
            "Skater squats asistidos": {
                description: "Sentadillas a una pierna con asistencia para equilibrio.",
                muscles: ["Cuádriceps", "Glúteos", "Isquiotibiales", "Core estabilizador"],
                recommendations: [
                    "Usa silla o barra para asistencia",
                    "Baja lentamente con control",
                    "Mantén torso erguido",
                    "Alterna piernas"
                ]
            },
            "Jump lunges": {
                description: "Estocadas con salto y cambio de pierna.",
                muscles: ["Cuádriceps", "Glúteos", "Isquiotibiales", "Pantorrillas"],
                recommendations: [
                    "Comienza en posición de estocada baja",
                    "Salta explosivamente cambiando piernas",
                    "Aterriza suavemente",
                    "Mantén core activado para estabilidad"
                ]
            },
            "Elevated calf raises": {
                description: "Elevaciones de talón con mayor rango de movimiento.",
                muscles: ["Gastrocnemio", "Sóleo", "Tibial posterior"],
                recommendations: [
                    "Eleva antepié sobre superficie",
                    "Baja talones lo máximo posible",
                    "Eleva hasta punta de pies",
                    "Pausa en contracción máxima"
                ]
            }
        };

        // Estado de la aplicación
        let appState = {
            currentPage: 'weeks',
            selectedWeek: 1,
            selectedDay: 'lunes',
            progress: {}
        };

        // Cargar el estado guardado
        function loadState() {
            try {
                const savedState = localStorage.getItem('calisthenicsProgress');
                if (savedState) {
                    appState.progress = JSON.parse(savedState);
                }
            } catch (e) {
                console.log("Error cargando estado");
                appState.progress = {};
            }
        }

        // Guardar el estado
        function saveState() {
            try {
                localStorage.setItem('calisthenicsProgress', JSON.stringify(appState.progress));
            } catch (e) {
                console.log("Error guardando estado");
            }
        }

        // Inicializar progreso de día
        function initDayProgress(weekId, day) {
            const key = `${weekId}-${day}`;
            if (!appState.progress[key]) {
                appState.progress[key] = {
                    completed: 0,
                    total: 0,
                    exercises: {}
                };
                saveState();
            }
        }

        // Actualizar progreso de ejercicio
        function updateExerciseProgress(weekId, day, exerciseIndex, setIndex, completed) {
            const key = `${weekId}-${day}`;
            
            if (!appState.progress[key]) {
                appState.progress[key] = {
                    completed: 0,
                    total: 0,
                    exercises: {}
                };
            }
            
            const week = trainingPlan.weeks.find(w => w.id == weekId);
            if (!week || !week.days[day]) return;
            
            const exercise = week.days[day].exercises[exerciseIndex];
            if (!exercise) return;
            
            if (!appState.progress[key].exercises[exerciseIndex]) {
                appState.progress[key].exercises[exerciseIndex] = new Array(exercise.sets).fill(false);
                appState.progress[key].total += exercise.sets;
            }
            
            const currentState = appState.progress[key].exercises[exerciseIndex][setIndex];
            appState.progress[key].exercises[exerciseIndex][setIndex] = completed;
            
            if (completed && !currentState) {
                appState.progress[key].completed++;
            } else if (!completed && currentState) {
                appState.progress[key].completed--;
            }
            
            saveState();
            updateDayProgressUI();
        }

        // Obtener progreso de día
        function getDayProgress(weekId, day) {
            const key = `${weekId}-${day}`;
            if (appState.progress[key]) {
                const progress = appState.progress[key];
                const percentage = progress.total > 0 ? 
                    Math.round((progress.completed / progress.total) * 100) : 0;
                return {
                    completed: progress.completed,
                    total: progress.total,
                    percentage: percentage
                };
            }
            return { completed: 0, total: 0, percentage: 0 };
        }

        // Obtener progreso de semana
        function getWeekProgress(weekId) {
            const week = trainingPlan.weeks.find(w => w.id == weekId);
            if (!week) return 0;
            
            let totalSets = 0;
            let completedSets = 0;
            
            for (const day in week.days) {
                const progress = getDayProgress(weekId, day);
                totalSets += progress.total;
                completedSets += progress.completed;
            }
            
            return totalSets > 0 ? Math.round((completedSets / totalSets) * 100) : 0;
        }

        // Reiniciar progreso de día
        function resetDayProgress() {
            const weekId = appState.selectedWeek;
            const day = appState.selectedDay;
            const key = `${weekId}-${day}`;
            
            if (appState.progress[key]) {
                for (let exIndex in appState.progress[key].exercises) {
                    const setsCount = appState.progress[key].exercises[exIndex].length;
                    appState.progress[key].exercises[exIndex] = new Array(setsCount).fill(false);
                }
                appState.progress[key].completed = 0;
                saveState();
                return true;
            }
            return false;
        }

        // Navegación entre páginas
        function navigateTo(page) {
            appState.currentPage = page;
            
            document.querySelectorAll('.page').forEach(p => {
                p.classList.remove('active');
            });
            
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            const pageElement = document.getElementById(`page-${page}`);
            if (pageElement) {
                pageElement.classList.add('active');
            }
            
            const btnElement = document.getElementById(`btn-${page}`);
            if (btnElement) {
                btnElement.classList.add('active');
            }
            
            if (page === 'weeks') {
                renderWeeks();
            } else if (page === 'days') {
                renderDays();
            } else if (page === 'exercises') {
                renderExercises();
            }
        }

        // Renderizar semanas
        function renderWeeks() {
            const container = document.getElementById('weeks-container');
            if (!container) return;
            
            container.innerHTML = '';
            
            for (let i = 1; i <= 52; i++) {
                const week = trainingPlan.weeks.find(w => w.id === i);
                if (!week) continue;
                
                const weekCard = document.createElement('div');
                weekCard.className = `week-card ${appState.selectedWeek === i ? 'active' : ''}`;
                weekCard.dataset.week = i;
                
                const weekProgress = getWeekProgress(i);
                
                weekCard.innerHTML = `
                    <h3>Semana ${i}</h3>
                    <p>${week.title}</p>
                    <div class="week-progress">
                        <div class="week-progress-bar" style="width: ${weekProgress}%"></div>
                    </div>
                `;
                
                weekCard.addEventListener('click', () => {
                    appState.selectedWeek = i;
                    renderWeeks();
                    navigateTo('days');
                });
                
                container.appendChild(weekCard);
            }
        }

        // Renderizar días
        function renderDays() {
            const weekId = appState.selectedWeek;
            const week = trainingPlan.weeks.find(w => w.id == weekId);
            if (!week) return;
            
            const titleElement = document.getElementById('current-week-title');
            if (titleElement) {
                titleElement.textContent = `Semana ${weekId}: ${week.title}`;
            }
            
            const container = document.getElementById('days-container');
            if (!container) return;
            
            container.innerHTML = '';
            
            const daysOrder = ['lunes', 'martes', 'miercoles', 'jueves', 'viernes'];
            
            daysOrder.forEach(dayKey => {
                const day = week.days[dayKey];
                if (!day) return;
                
                const dayProgress = getDayProgress(weekId, dayKey);
                
                const dayCard = document.createElement('div');
                dayCard.className = `day-card ${appState.selectedDay === dayKey ? 'active' : ''}`;
                dayCard.dataset.day = dayKey;
                
                let dayIcon = 'fas fa-dumbbell';
                if (dayKey === 'martes') dayIcon = 'fas fa-heart';
                if (dayKey === 'miercoles') dayIcon = 'fas fa-hands';
                if (dayKey === 'jueves') dayIcon = 'fas fa-sync-alt';
                if (dayKey === 'viernes') dayIcon = 'fas fa-running';
                
                dayCard.innerHTML = `
                    <div class="day-icon">
                        <i class="${dayIcon}"></i>
                    </div>
                    <h3>${day.title}</h3>
                    <p>${day.exercises.length} ejercicios</p>
                    <div class="week-progress">
                        <div class="week-progress-bar" style="width: ${dayProgress.percentage}%"></div>
                    </div>
                `;
                
                dayCard.addEventListener('click', () => {
                    appState.selectedDay = dayKey;
                    initDayProgress(weekId, dayKey);
                    navigateTo('exercises');
                });
                
                container.appendChild(dayCard);
            });
        }

        // Renderizar ejercicios
        function renderExercises() {
            const weekId = appState.selectedWeek;
            const dayKey = appState.selectedDay;
            const week = trainingPlan.weeks.find(w => w.id == weekId);
            if (!week) return;
            
            const day = week.days[dayKey];
            if (!day) return;
            
            const dayTitleElement = document.getElementById('day-title');
            if (dayTitleElement) {
                dayTitleElement.textContent = day.title;
            }
            
            const weekSubtitleElement = document.getElementById('week-subtitle');
            if (weekSubtitleElement) {
                weekSubtitleElement.textContent = `Semana ${weekId}: ${week.title}`;
            }
            
            updateDayProgressUI();
            
            const container = document.getElementById('exercises-container');
            if (!container) return;
            
            container.innerHTML = '';
            
            initDayProgress(weekId, dayKey);
            
            const progressKey = `${weekId}-${dayKey}`;
            const dayProgress = appState.progress[progressKey] || {
                completed: 0,
                total: 0,
                exercises: {}
            };
            
            day.exercises.forEach((exercise, exIndex) => {
                const info = exerciseInfo[exercise.name] || {
                    description: `Ejercicio de ${exercise.type} para desarrollar fuerza y resistencia.`,
                    muscles: ["Músculos principales según el tipo de ejercicio"],
                    recommendations: [
                        "Mantén la forma adecuada durante todo el movimiento",
                        "Controla la respiración: exhala en el esfuerzo, inhala en la relajación",
                        "No sacrifiques la técnica por hacer más repeticiones",
                        "Descansa lo suficiente entre series"
                    ]
                };
                
                let muscles = info.muscles;
                if (!exerciseInfo[exercise.name]) {
                    switch(exercise.type) {
                        case 'push': muscles = ["Pectoral", "Tríceps", "Deltoides anterior"]; break;
                        case 'pull': muscles = ["Dorsal", "Bíceps", "Trapecio"]; break;
                        case 'legs': muscles = ["Cuádriceps", "Glúteos", "Isquiotibiales"]; break;
                        case 'core': muscles = ["Recto abdominal", "Oblicuos", "Transverso abdominal"]; break;
                        case 'cardio': muscles = ["Sistema cardiovascular", "Piernas"]; break;
                        case 'flex': muscles = ["Todos los grupos musculares"]; break;
                        case 'recovery': muscles = ["Sistema nervioso", "Músculos en recuperación"]; break;
                        case 'mixed': muscles = ["Músculos variados según ejercicio"]; break;
                        default: muscles = ["Músculos variados según el ejercicio"];
                    }
                }
                
                let setsButtons = '';
                const exerciseProgress = dayProgress.exercises[exIndex] || new Array(exercise.sets).fill(false);
                
                for (let i = 0; i < exercise.sets; i++) {
                    const isCompleted = exerciseProgress[i] || false;
                    setsButtons += `
                        <button class="set-btn ${isCompleted ? 'completed' : ''}" 
                                data-set="${i}" 
                                data-exercise="${exIndex}">
                            ${i + 1}
                        </button>
                    `;
                }
                
                const exerciseCard = document.createElement('div');
                exerciseCard.className = 'exercise-card';
                exerciseCard.innerHTML = `
                    <div class="exercise-header">
                        <div class="exercise-name">${exercise.name}</div>
                        <button class="exercise-info-btn" data-exercise="${exercise.name}">
                            i
                        </button>
                    </div>
                    <div class="exercise-details">
                        <div class="exercise-sets">${exercise.sets} x ${exercise.reps}</div>
                        <div class="exercise-muscles">${exercise.type.toUpperCase()}</div>
                    </div>
                    <div class="sets-container">
                        ${setsButtons}
                    </div>
                `;
                
                container.appendChild(exerciseCard);
            });
            
            document.querySelectorAll('.exercise-info-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const exerciseName = btn.getAttribute('data-exercise');
                    showExerciseModal(exerciseName);
                });
            });
            
            document.querySelectorAll('.set-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const setIndex = parseInt(btn.getAttribute('data-set'));
                    const exerciseIndex = parseInt(btn.getAttribute('data-exercise'));
                    const isCompleted = btn.classList.contains('completed');
                    
                    const newState = !isCompleted;
                    
                    updateExerciseProgress(
                        weekId, 
                        dayKey, 
                        exerciseIndex, 
                        setIndex, 
                        newState
                    );
                    
                    btn.classList.toggle('completed');
                    updateDayProgressUI();
                });
            });
        }

        // Actualizar UI de progreso
        function updateDayProgressUI() {
            const weekId = appState.selectedWeek;
            const dayKey = appState.selectedDay;
            const progress = getDayProgress(weekId, dayKey);
            
            const progressText = document.getElementById('progress-text');
            const progressFill = document.getElementById('day-progress-fill');
            
            if (progressText) {
                progressText.textContent = `${progress.percentage}% completado`;
            }
            
            if (progressFill) {
                progressFill.style.width = `${progress.percentage}%`;
            }
        }

        // Mostrar modal de ejercicio
        function showExerciseModal(exerciseName) {
            const info = exerciseInfo[exerciseName] || {
                description: `Ejercicio de calistenia para desarrollar fuerza y resistencia.`,
                muscles: ["Músculos principales según el tipo de ejercicio"],
                recommendations: [
                    "Mantén la forma adecuada durante todo el movimiento",
                    "Controla la respiración: exhala en el esfuerzo, inhala en la relajación",
                    "No sacrifiques la técnica por hacer más repeticiones",
                    "Descansa lo suficiente entre series"
                ]
            };
            
            const modalName = document.getElementById('modal-exercise-name');
            if (modalName) modalName.textContent = exerciseName;
            
            const modalDesc = document.getElementById('modal-description');
            if (modalDesc) modalDesc.textContent = info.description;
            
            const musclesList = document.getElementById('modal-muscles');
            if (musclesList) {
                musclesList.innerHTML = '';
                info.muscles.forEach(muscle => {
                    const li = document.createElement('li');
                    li.textContent = muscle;
                    musclesList.appendChild(li);
                });
            }
            
            const recList = document.getElementById('modal-recommendations');
            if (recList) {
                recList.innerHTML = '';
                info.recommendations.forEach(rec => {
                    const li = document.createElement('li');
                    li.textContent = rec;
                    recList.appendChild(li);
                });
            }
            
            const modal = document.getElementById('exercise-modal');
            if (modal) {
                modal.classList.add('active');
            }
        }

        // Inicializar aplicación
        function initApp() {
            loadState();
            renderWeeks();
            
            document.getElementById('btn-weeks').addEventListener('click', () => navigateTo('weeks'));
            document.getElementById('btn-days').addEventListener('click', () => navigateTo('days'));
            document.getElementById('btn-exercises').addEventListener('click', () => navigateTo('exercises'));
            
            document.getElementById('btn-back-to-weeks').addEventListener('click', () => navigateTo('weeks'));
            document.getElementById('btn-back-to-days').addEventListener('click', () => navigateTo('days'));
            
            document.getElementById('btn-reset-day').addEventListener('click', () => {
                if (confirm('¿Estás seguro de que quieres reiniciar el progreso de este día?')) {
                    resetDayProgress();
                    renderExercises();
                }
            });
            
            document.getElementById('modal-close-btn').addEventListener('click', () => {
                const modal = document.getElementById('exercise-modal');
                if (modal) {
                    modal.classList.remove('active');
                }
            });
            
            const modal = document.getElementById('exercise-modal');
            if (modal) {
                modal.addEventListener('click', (e) => {
                    if (e.target === modal) {
                        modal.classList.remove('active');
                    }
                });
            }
        }

        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>

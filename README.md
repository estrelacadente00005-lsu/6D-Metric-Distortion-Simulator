<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Distorção de Métrica Espacial 6D - Encolhimento & Ampliação Relativística</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800;900&family=Rajdhani:wght@300;500;600;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyan: { neon: '#00f3ff' },
                        magenta: { neon: '#ff0055' },
                        gold: { neon: '#ffb700' },
                        purple: { neon: '#b000ff' },
                        emerald: { neon: '#00ff66' }
                    },
                    fontFamily: {
                        orbitron: ['Orbitron', 'sans-serif'],
                        rajdhani: ['Rajdhani', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #02040a;
            color: #e2e8f0;
            font-family: 'Rajdhani', sans-serif;
            overflow-x: hidden;
        }

        /* Glassmorphism Sci-Fi HUD */
        .hud-panel {
            background: rgba(5, 10, 24, 0.88);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(0, 243, 255, 0.25);
            box-shadow: 0 0 30px rgba(0, 243, 255, 0.06), inset 0 0 15px rgba(0, 243, 255, 0.03);
        }

        .hud-title {
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 0.08em;
            text-transform: uppercase;
        }

        /* Scanline Overlay Effect */
        .scanline {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 0, 0, 0.4) 50%,
                rgba(0, 0, 0, 0.4)
            );
            background-size: 100% 4px;
            pointer-events: none;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #02040a;
        }
        ::-webkit-scrollbar-thumb {
            background: #00f3ff;
            border-radius: 3px;
        }

        /* Custom Range Inputs */
        input[type=range] {
            accent-color: #00f3ff;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-cyan-500 selection:text-black">

    <!-- OVERLAY SCANLINES FOR SCI-FI ATMOSPHERE -->
    <div class="fixed inset-0 scanline z-40 opacity-30 pointer-events-none"></div>

    <!-- TOP HEADER / NAV -->
    <header class="relative z-30 w-full px-4 py-3 bg-slate-950/90 border-b border-cyan-500/30 backdrop-blur-md flex flex-wrap items-center justify-between gap-4">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-lg border border-cyan-400/60 bg-cyan-950/40 flex items-center justify-center text-cyan-400 text-xl shadow-[0_0_15px_rgba(0,243,255,0.4)]">
                <i class="fa-solid fa-compress-arrows-alt animate-pulse"></i>
            </div>
            <div>
                <h1 class="hud-title text-base md:text-xl font-black bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 via-purple-400 to-gold-400">
                    DISTORÇÃO DE MÉTRICA ESPACIAL 6D
                </h1>
                <p class="text-xs text-slate-400 flex items-center gap-2">
                    <span class="inline-block w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                    TECNOLOGIA DE ENCOLHIMENTO E AMPLIAÇÃO RELATIVÍSTICA (1G SAMS)
                </p>
            </div>
        </div>

        <!-- CAMERA POV SWITCH & INFO BUTTON -->
        <div class="flex items-center gap-3 flex-wrap">
            <div class="bg-slate-900/90 p-1 rounded-xl border border-slate-800 flex items-center gap-1">
                <button id="btnPovExternal" class="px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-cyan-500 text-slate-950 shadow-[0_0_10px_rgba(0,243,255,0.5)]">
                    <i class="fa-solid fa-eye mr-1"></i> POV Observador Externo
                </button>
                <button id="btnPovPilot" class="px-3 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-white">
                    <i class="fa-solid fa-user-astronaut mr-1"></i> POV Cockpit (Visão Interna)
                </button>
            </div>

            <button id="btnOverview" class="px-3.5 py-2 rounded-lg bg-slate-900/90 hover:bg-cyan-950/60 border border-cyan-500/50 text-cyan-300 font-semibold text-xs md:text-sm transition-all shadow-[0_0_15px_rgba(0,243,255,0.2)] flex items-center gap-2">
                <i class="fa-solid fa-book-journal-whills text-cyan-400"></i>
                Visão Geral & Física Relativística
            </button>
        </div>
    </header>

    <!-- MAIN DASHBOARD LAYOUT -->
    <main class="relative z-10 flex-1 grid grid-cols-1 lg:grid-cols-12 gap-4 p-4 max-w-[1920px] mx-auto w-full">

        <!-- LEFT PANEL: PRESETS & SCALE CONTROL (3 COLS) -->
        <section class="lg:col-span-3 flex flex-col gap-4">

            <!-- PRESETS -->
            <div class="hud-panel rounded-xl p-4">
                <h2 class="hud-title text-xs text-cyan-400 mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-sliders text-purple-400"></i> Pré-Ajustes Rápidos de Escala
                </h2>
                <div class="grid grid-cols-2 gap-2">
                    <button data-scale="1e-9" class="btn-preset p-2.5 rounded-lg border border-slate-800 bg-slate-900/50 hover:bg-purple-950/40 hover:border-purple-500/50 transition-all text-left">
                        <div class="text-xs font-bold text-purple-300">Quântico</div>
                        <div class="text-[10px] text-slate-400">10⁻⁹m (Átomos)</div>
                    </button>
                    <button data-scale="1e-3" class="btn-preset p-2.5 rounded-lg border border-cyan-500/50 bg-cyan-950/30 text-left active-preset">
                        <div class="text-xs font-bold text-cyan-300">Formiga</div>
                        <div class="text-[10px] text-slate-400">10⁻³m (Micro)</div>
                    </button>
                    <button data-scale="1.8" class="btn-preset p-2.5 rounded-lg border border-slate-800 bg-slate-900/50 hover:bg-emerald-950/40 hover:border-emerald-500/50 transition-all text-left">
                        <div class="text-xs font-bold text-emerald-300">Humano 1G</div>
                        <div class="text-[10px] text-slate-400">1.8m (Escala Real)</div>
                    </button>
                    <button data-scale="1e3" class="btn-preset p-2.5 rounded-lg border border-slate-800 bg-slate-900/50 hover:bg-gold-950/40 hover:border-gold-500/50 transition-all text-left">
                        <div class="text-xs font-bold text-gold-300">Titan</div>
                        <div class="text-[10px] text-slate-400">1000m (Macro)</div>
                    </button>
                </div>
            </div>

            <!-- SLIDERS & PARAMETERS -->
            <div class="hud-panel rounded-xl p-4 flex-1 flex flex-col justify-between">
                <div>
                    <h2 class="hud-title text-xs text-purple-400 mb-3 flex items-center justify-between">
                        <span><i class="fa-solid fa-gauge-high text-cyan-400 mr-1.5"></i> Métrica & Campo 6D</span>
                    </h2>

                    <div class="space-y-4 text-xs">
                        <!-- LOGARITHMIC SCALE SLIDER -->
                        <div class="p-3 rounded-lg border border-cyan-500/30 bg-cyan-950/10">
                            <div class="flex justify-between mb-1">
                                <span class="font-bold text-cyan-300">Fator de Escala Métrica (η):</span>
                                <span id="valScaleText" class="font-mono text-cyan-200">1.00 x 10⁻³ m</span>
                            </div>
                            <input type="range" id="sliderScale" min="-9" max="3" step="0.01" value="-3" class="w-full">
                            <div class="flex justify-between text-[9px] text-slate-500 mt-1 font-mono">
                                <span>10⁻⁹m</span>
                                <span>10⁻³m</span>
                                <span>1.8m</span>
                                <span>10³m</span>
                            </div>
                        </div>

                        <!-- SAMS FIELD (GRAVITY STABILITY) -->
                        <div class="p-3 rounded-lg border border-emerald-500/30 bg-emerald-950/10">
                            <div class="flex justify-between mb-1">
                                <span class="font-bold text-emerald-300 flex items-center gap-1.5">
                                    <i class="fa-solid fa-shield-halved text-emerald-400"></i> Amortecimento SAMS:
                                </span>
                                <span id="valSamsText" class="font-mono text-emerald-200">1.00 G (Travado)</span>
                            </div>
                            <input type="range" id="sliderSams" min="0.5" max="2.0" step="0.01" value="1.0" class="w-full">
                            <span class="text-[10px] text-slate-400 mt-1 block">Preserva gravidade e densidade biológica interna constantes.</span>
                        </div>

                        <!-- SROS FREQUENCY -->
                        <div class="p-3 rounded-lg border border-purple-500/30 bg-purple-950/10">
                            <div class="flex justify-between mb-1">
                                <span class="font-bold text-purple-300 flex items-center gap-1.5">
                                    <i class="fa-solid fa-wave-square text-purple-400"></i> Frequência de Fase SROS:
                                </span>
                                <span id="valSrosText" class="font-mono text-purple-200">432.8 THz</span>
                            </div>
                            <input type="range" id="sliderSros" min="100" max="900" step="1" value="432" class="w-full">
                        </div>

                        <!-- MHD POWER -->
                        <div class="p-3 rounded-lg border border-amber-500/30 bg-amber-950/10">
                            <div class="flex justify-between mb-1">
                                <span class="font-bold text-amber-300 flex items-center gap-1.5">
                                    <i class="fa-solid fa-bolt text-amber-400"></i> Potência MHD do Traje:
                                </span>
                                <span id="valMhdText" class="font-mono text-amber-200">98.5 MW</span>
                            </div>
                            <input type="range" id="sliderMhd" min="10" max="500" step="1" value="98" class="w-full">
                        </div>
                    </div>
                </div>

                <div class="mt-4 p-2.5 rounded-lg border border-cyan-500/40 bg-cyan-950/20 text-cyan-300 text-[11px] flex items-center gap-2">
                    <i class="fa-solid fa-atom text-cyan-400 text-sm animate-spin"></i>
                    <span>Geometria métrica local reconfigurada. Matéria livre de esmagamento atômico.</span>
                </div>
            </div>

        </section>

        <!-- CENTER PANEL: HIGH-PERFORMANCE CANVAS 2D (6 COLS) -->
        <section class="lg:col-span-6 flex flex-col gap-3 min-h-[480px] lg:min-h-0">
            <div id="canvasContainer" class="relative flex-1 hud-panel rounded-xl overflow-hidden flex flex-col border border-cyan-500/30">
                
                <!-- CANVAS TOP OVERLAY HUD -->
                <div class="absolute top-3 left-3 right-3 z-20 flex items-center justify-between pointer-events-none">
                    <div class="flex items-center gap-2 bg-slate-950/85 px-3 py-1.5 rounded-lg border border-slate-800">
                        <span id="pingDot" class="w-2.5 h-2.5 rounded-full bg-cyan-400 animate-ping"></span>
                        <span id="lblPovTitle" class="text-xs font-bold text-cyan-300 font-mono">OBSERVADOR EXTERNO (LABORATÓRIO)</span>
                    </div>
                    <div class="text-xs text-slate-400 font-mono bg-slate-950/85 px-3 py-1.5 rounded-lg border border-slate-800 flex items-center gap-3">
                        <span>REFERÊNCIA: <strong id="lblRefObject" class="text-purple-300">Formiga (2.5mm) / Tecido Espaço-Tempo</strong></span>
                        <span>FPS: <strong id="fpsCounter" class="text-emerald-400">60</strong></span>
                    </div>
                </div>

                <!-- CANVAS ELEMENT -->
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair bg-slate-950"></canvas>

                <!-- CANVAS BOTTOM FOOTER OVERLAY -->
                <div class="p-3 bg-slate-950/90 border-t border-slate-800 flex items-center justify-between z-20 text-xs">
                    <div class="flex items-center gap-4">
                        <span class="text-slate-400"><i class="fa-solid fa-circle text-[8px] text-cyan-400 mr-1"></i> Bolha Métrica 6D</span>
                        <span class="text-slate-400"><i class="fa-solid fa-circle text-[8px] text-amber-400 mr-1"></i> Feixes MHD/SROS</span>
                        <span class="text-slate-400"><i class="fa-solid fa-circle text-[8px] text-purple-400 mr-1"></i> Amortecedor SAMS</span>
                    </div>
                    <div class="font-mono text-slate-400">
                        Massa do Traje: <strong class="text-slate-200">82.0 kg (Invariável)</strong>
                    </div>
                </div>
            </div>
        </section>

        <!-- RIGHT PANEL: TELEMETRY & PHYSICAL METRICS (3 COLS) -->
        <section class="lg:col-span-3 flex flex-col gap-4">

            <!-- TELEMETRY METRICS -->
            <div class="hud-panel rounded-xl p-4 space-y-3">
                <h2 class="hud-title text-xs text-cyan-400 mb-1 flex items-center gap-2">
                    <i class="fa-solid fa-chart-pie text-cyan-400"></i> Telemetria Métrica & Gravitacional
                </h2>

                <!-- METRIC 1: DENSITY (LOCAL VS APPARENT) -->
                <div class="bg-slate-900/60 p-2.5 rounded-lg border border-slate-800">
                    <div class="flex justify-between text-xs mb-1">
                        <span class="text-slate-400">Densidade Biológica Interna:</span>
                        <span id="metricInternalDensity" class="text-emerald-400 font-mono font-bold">1.00 g/cm³</span>
                    </div>
                    <div class="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden">
                        <div class="bg-emerald-400 h-full w-full"></div>
                    </div>
                    <span class="text-[9px] text-emerald-400/80 mt-1 block">✔ Zero compressão atômica (Prótons preservados)</span>
                </div>

                <!-- METRIC 2: APPARENT DENSITY EXTERNAL -->
                <div class="bg-slate-900/60 p-2.5 rounded-lg border border-slate-800">
                    <div class="flex justify-between text-xs mb-1">
                        <span class="text-slate-400">Densidade Aparente Externa:</span>
                        <span id="metricExternalDensity" class="text-purple-300 font-mono font-bold">8.20 x 10⁴ g/cm³</span>
                    </div>
                    <div class="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden">
                        <div id="barApparentDensity" class="bg-purple-400 h-full transition-all duration-300" style="width: 45%;"></div>
                    </div>
                </div>

                <!-- METRIC 3: SPACETIME CURVATURE (G_mu_nu) -->
                <div class="bg-slate-900/60 p-2.5 rounded-lg border border-slate-800">
                    <div class="flex justify-between text-xs mb-1">
                        <span class="text-slate-400">Curvatura Métrica (G<sub>μν</sub>):</span>
                        <span id="metricCurvature" class="text-cyan-300 font-mono font-bold">3.42 x 10³ m⁻²</span>
                    </div>
                    <div class="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden">
                        <div id="barCurvature" class="bg-cyan-400 h-full transition-all duration-300" style="width: 30%;"></div>
                    </div>
                </div>

                <!-- METRIC 4: SINGULARITY COLLAPSE RISK -->
                <div class="bg-slate-900/60 p-2.5 rounded-lg border border-slate-800">
                    <div class="flex justify-between text-xs mb-1">
                        <span class="text-slate-400">Risco de Micro-Buraco Negro:</span>
                        <span id="metricSingularityRisk" class="text-emerald-400 font-mono font-bold">0.000 % (Nulo)</span>
                    </div>
                    <div class="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden">
                        <div class="bg-emerald-400 h-full w-[1%]"></div>
                    </div>
                </div>
            </div>

            <!-- HARDWARE STATUS & PILOT STATE -->
            <div class="hud-panel rounded-xl p-4 flex-1 flex flex-col justify-between">
                <div>
                    <h2 class="hud-title text-xs text-purple-400 mb-2 flex items-center justify-between">
                        <span><i class="fa-solid fa-microchip text-purple-400 mr-1.5"></i> Subsistemas do Traje 6D</span>
                    </h2>

                    <div class="space-y-2 text-xs">
                        <div class="p-2 rounded border border-emerald-500/30 bg-emerald-950/10 flex items-center justify-between">
                            <span class="text-slate-300 flex items-center gap-2">
                                <i class="fa-solid fa-circle-check text-emerald-400"></i> Matriz SAMS (1G Lock)
                            </span>
                            <span class="text-emerald-400 font-bold font-mono">ATIVO</span>
                        </div>
                        <div class="p-2 rounded border border-emerald-500/30 bg-emerald-950/10 flex items-center justify-between">
                            <span class="text-slate-300 flex items-center gap-2">
                                <i class="fa-solid fa-circle-check text-emerald-400"></i> Lasers SROS (Escalar)
                            </span>
                            <span class="text-emerald-400 font-bold font-mono">SINCRONIZADO</span>
                        </div>
                        <div class="p-2 rounded border border-emerald-500/30 bg-emerald-950/10 flex items-center justify-between">
                            <span class="text-slate-300 flex items-center gap-2">
                                <i class="fa-solid fa-circle-check text-emerald-400"></i> Micro-Conductores MHD
                            </span>
                            <span class="text-emerald-400 font-bold font-mono">ESTÁVEL</span>
                        </div>
                        <div class="p-2 rounded border border-emerald-500/30 bg-emerald-950/10 flex items-center justify-between">
                            <span class="text-slate-300 flex items-center gap-2">
                                <i class="fa-solid fa-circle-check text-emerald-400"></i> Injetor Singularidade 6D
                            </span>
                            <span class="text-emerald-400 font-bold font-mono">OPERACIONAL</span>
                        </div>
                    </div>
                </div>

                <div class="mt-4 pt-3 border-t border-slate-800 text-[11px] text-slate-400 flex items-center justify-between">
                    <span class="flex items-center gap-1.5"><i class="fa-solid fa-heart-pulse text-red-400"></i> Vital do Piloto:</span>
                    <span class="font-mono text-cyan-300">72 BPM / Estável</span>
                </div>
            </div>

        </section>

    </main>

    <!-- FOOTER HUD -->
    <footer class="relative z-30 px-4 py-2 bg-slate-950/90 border-t border-slate-900 text-slate-500 text-xs flex justify-between items-center">
        <div>Engenharia Métrica 6D © 2026 — Projeto SAMS/SROS/MHD Unificado</div>
        <div class="flex gap-4">
            <span class="text-cyan-400"><i class="fa-solid fa-expand-arrows-alt mr-1"></i> Space Metric: Curved</span>
            <span class="text-emerald-400"><i class="fa-solid fa-shield-halved mr-1"></i> SAMS 1G Protective Bubble</span>
        </div>
    </footer>

    <!-- OVERVIEW & SCIENTIFIC MODAL -->
    <div id="overviewModal" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-300">
        <div class="hud-panel w-full max-w-4xl max-h-[90vh] rounded-2xl border border-cyan-500/40 p-6 flex flex-col overflow-hidden shadow-[0_0_50px_rgba(0,243,255,0.25)]">
            
            <!-- MODAL HEADER -->
            <div class="flex justify-between items-center border-b border-cyan-500/30 pb-4 mb-4">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-lg bg-cyan-500/20 border border-cyan-400 flex items-center justify-center text-cyan-300 text-xl">
                        <i class="fa-solid fa-atom"></i>
                    </div>
                    <div>
                        <h2 class="hud-title text-lg font-bold text-cyan-300">Física Métrica 6D vs HQs da Marvel</h2>
                        <p class="text-xs text-slate-400">Reconfiguração Relativística do Espaço-Tempo sem Colapso Gravitacional</p>
                    </div>
                </div>
                <button id="btnCloseModal" class="text-slate-400 hover:text-white text-2xl p-2 transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- MODAL CONTENT (SCROLLABLE) -->
            <div class="flex-1 overflow-y-auto pr-2 space-y-5 text-sm text-slate-300 leading-relaxed">
                
                <!-- COMPARATIVE BOX -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="p-4 rounded-xl bg-magenta-950/20 border border-magenta-500/30">
                        <h3 class="font-bold text-magenta-300 text-sm flex items-center gap-2 mb-2">
                            <i class="fa-solid fa-book-open"></i> O Erro das HQs (Homem-Formiga)
                        </h3>
                        <p class="text-xs text-slate-300 leading-normal">
                            Nas HQs, o encolhimento aproxima os átomos mantendo a massa original. Se um adulto de 80kg encolhesse para 2 milímetros aproximando prótons e elétrons, sua densidade atingiria <strong class="text-magenta-300">10¹³ g/cm³</strong>, gerando uma pressão de perfuração infinita no solo e colapsando em um <strong>micro-buraco negro</strong> instantâneo.
                        </p>
                    </div>

                    <div class="p-4 rounded-xl bg-cyan-950/20 border border-cyan-500/30">
                        <h3 class="font-bold text-cyan-300 text-sm flex items-center gap-2 mb-2">
                            <i class="fa-solid fa-flask"></i> A Solução Científica 6D Real
                        </h3>
                        <p class="text-xs text-slate-300 leading-normal">
                            A Impressora 6D e o traje criam uma <strong>Bolha de Distorção Métrica Espacial de 6ª Dimensão</strong>. O espaço interior mantém tamanho 1:1, gravidade 1G (via SAMS) e distância atômica natural. É o próprio tecido espaço-temporal ao redor que é comprimido ou expandido em relação ao observador externo.
                        </p>
                    </div>
                </div>

                <!-- DIAGRAM ASCII -->
                <div class="bg-slate-950 p-4 rounded-xl border border-cyan-500/30 font-mono text-xs text-cyan-300 overflow-x-auto">
                    <pre class="leading-tight">
┌────────────────────────────────────────────────────────────────────────┐
│                   BOLHA MÉTRICA 6D (TRAJE RELATIVÍSTICO)               │
├────────────────────────────────────────────────────────────────────────┤
│ Micro-Condutores MHD  ──> Alimenta o campo com plasma ressonante       │
│ SAMS Dimensional      ──> Amortecimento piezoelétrico (Mantém 1G)     │
│ SROS Lasers           ──> Sincroniza feixes de fase de escala métrica │
│ Impressora Quântica 6D──> Reorganiza a geometria métrica do vácuo      │
└────────────────────────────────────────────────────────────────────────┘
                    </pre>
                </div>

                <!-- FIVE PILLARS DETAILED -->
                <div class="space-y-3">
                    <h3 class="hud-title text-xs text-purple-400">Os 5 Pilares do Traje 6D:</h3>
                    
                    <div class="p-3 rounded-lg bg-slate-900/60 border border-slate-800 text-xs">
                        <strong class="text-cyan-300">1. Mecanismo de Singularidade Direcionada:</strong> Cria o gradiente de curvatura necessário para distorcer a métrica espacial em 6 dimensões.
                    </div>
                    <div class="p-3 rounded-lg bg-slate-900/60 border border-slate-800 text-xs">
                        <strong class="text-emerald-300">2. SAMS Dimensional (1G Gravity Bubble):</strong> Impede que o piloto sinta a distorção externa. Dentro da bolha, a gravidade e o tamanho dos tecidos biológicos permanecem inalterados.
                    </div>
                    <div class="p-3 rounded-lg bg-slate-900/60 border border-slate-800 text-xs">
                        <strong class="text-purple-300">3. SROS (Fase Escalar):</strong> Mede e estabiliza a razão de compressão da escala métrica ($\eta$) para evitar oscilações de tamanho.
                    </div>
                    <div class="p-3 rounded-lg bg-slate-900/60 border border-slate-800 text-xs">
                        <strong class="text-amber-300">4. Micro-Condutores MHD:</strong> Fornecem a densidade de energia magnética necessária para manter a bolha estável contra perturbações externas.
                    </div>
                    <div class="p-3 rounded-lg bg-slate-900/60 border border-slate-800 text-xs">
                        <strong class="text-magenta-300">5. Impressora Quântica 6D:</strong> Modula as propriedades métricas do vácuo ao redor da fuselagem do traje em tempo real.
                    </div>
                </div>

            </div>

            <!-- MODAL FOOTER -->
            <div class="mt-4 pt-3 border-t border-cyan-500/30 flex justify-end">
                <button id="btnDismissModal" class="px-5 py-2 rounded-lg bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold text-sm transition-all shadow-[0_0_15px_rgba(0,243,255,0.4)]">
                    Entendido / Voltar ao Simulador
                </button>
            </div>

        </div>
    </div>

    <!-- JAVASCRIPT ANIMATION ENGINE & SIMULATION LOGIC -->
    <script>
        window.onload = function() {
            const canvas = document.getElementById('simCanvas');
            const ctx = canvas.getContext('2d');

            // SIMULATION STATE ENGINE
            const state = {
                pov: 'external', // 'external' or 'pilot'
                scaleExponent: -3, // -9 to 3 (slider log scale)
                scaleFactor: 1e-3, // calculated scale metric (meters)
                samsG: 1.0,
                srosFreq: 432,
                mhdPower: 98,
                time: 0,
                
                // Animated suit position
                suitPos: { x: 0, y: 0 },
                
                // Reference Objects
                antPos: { x: 120, y: 40 },
                atomPos: { x: -100, y: -50 }
            };

            // Canvas Resize Handler
            function resizeCanvas() {
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
            }
            window.addEventListener('resize', resizeCanvas);
            resizeCanvas();

            // EVENT LISTENERS: CAMERA POV
            document.getElementById('btnPovExternal').addEventListener('click', () => {
                state.pov = 'external';
                document.getElementById('btnPovExternal').className = "px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-cyan-500 text-slate-950 shadow-[0_0_10px_rgba(0,243,255,0.5)]";
                document.getElementById('btnPovPilot').className = "px-3 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-white";
                document.getElementById('lblPovTitle').innerText = "OBSERVADOR EXTERNO (LABORATÓRIO)";
            });

            document.getElementById('btnPovPilot').addEventListener('click', () => {
                state.pov = 'pilot';
                document.getElementById('btnPovPilot').className = "px-3 py-1.5 rounded-lg text-xs font-bold transition-all bg-cyan-500 text-slate-950 shadow-[0_0_10px_rgba(0,243,255,0.5)]";
                document.getElementById('btnPovExternal').className = "px-3 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-white";
                document.getElementById('lblPovTitle').innerText = "POV PILOTO (VISÃO INTERNA DA BOLHA 1G)";
            });

            // PRESET BUTTONS
            document.querySelectorAll('.btn-preset').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    document.querySelectorAll('.btn-preset').forEach(b => {
                        b.classList.remove('border-cyan-500/50', 'bg-cyan-950/30', 'active-preset');
                        b.classList.add('border-slate-800', 'bg-slate-900/50');
                    });
                    const target = e.currentTarget;
                    target.classList.remove('border-slate-800', 'bg-slate-900/50');
                    target.classList.add('border-cyan-500/50', 'bg-cyan-950/30', 'active-preset');

                    const scaleVal = parseFloat(target.getAttribute('data-scale'));
                    state.scaleFactor = scaleVal;
                    state.scaleExponent = Math.log10(scaleVal);
                    document.getElementById('sliderScale').value = state.scaleExponent;
                    updateUI();
                });
            });

            // SLIDERS
            document.getElementById('sliderScale').addEventListener('input', (e) => {
                state.scaleExponent = parseFloat(e.target.value);
                state.scaleFactor = Math.pow(10, state.scaleExponent);
                updateUI();
            });

            document.getElementById('sliderSams').addEventListener('input', (e) => {
                state.samsG = parseFloat(e.target.value);
                document.getElementById('valSamsText').innerText = `${state.samsG.toFixed(2)} G`;
            });

            document.getElementById('sliderSros').addEventListener('input', (e) => {
                state.srosFreq = parseInt(e.target.value);
                document.getElementById('valSrosText').innerText = `${state.srosFreq} THz`;
            });

            document.getElementById('sliderMhd').addEventListener('input', (e) => {
                state.mhdPower = parseInt(e.target.value);
                document.getElementById('valMhdText').innerText = `${state.mhdPower} MW`;
            });

            // MODAL CONTROLS
            const modal = document.getElementById('overviewModal');
            document.getElementById('btnOverview').addEventListener('click', () => modal.classList.remove('opacity-0', 'pointer-events-none'));
            document.getElementById('btnCloseModal').addEventListener('click', () => modal.classList.add('opacity-0', 'pointer-events-none'));
            document.getElementById('btnDismissModal').addEventListener('click', () => modal.classList.add('opacity-0', 'pointer-events-none'));

            function updateUI() {
                // Formatting scale factor string
                let scaleStr = "";
                if (state.scaleFactor >= 1) {
                    scaleStr = `${state.scaleFactor.toFixed(1)} m`;
                } else {
                    scaleStr = `1.00 x 10${state.scaleExponent.toFixed(1)} m`;
                }
                document.getElementById('valScaleText').innerText = scaleStr;

                // Update Apparent Density
                const normScale = state.scaleFactor / 1.8;
                const apparentDensity = (1.0 / Math.pow(normScale, 3)).toExponential(2);
                document.getElementById('metricExternalDensity').innerText = `${apparentDensity} g/cm³`;

                // Curvature G_mu_nu
                const curvature = (Math.abs(Math.log10(state.scaleFactor)) * 1.25e3).toExponential(2);
                document.getElementById('metricCurvature').innerText = `${curvature} m⁻²`;

                // Reference Object Label
                const refLbl = document.getElementById('lblRefObject');
                if (state.scaleFactor < 1e-6) {
                    refLbl.innerText = "Átomo de Hidrogênio (0.1nm) / Núcleo";
                } else if (state.scaleFactor < 0.1) {
                    refLbl.innerText = "Formiga Operária (2.5mm) / Bancada";
                } else if (state.scaleFactor <= 10) {
                    refLbl.innerText = "Ser Humano (1.8m) / Laboratório";
                } else {
                    refLbl.innerText = "Arranha-Céu / Megaestrutura (1000m)";
                }
            }

            // FPS Counter Variables
            let lastTime = performance.now();
            let frameCount = 0;

            // MAIN ANIMATION LOOP (60 FPS)
            function animate(now) {
                frameCount++;
                if (now - lastTime >= 1000) {
                    document.getElementById('fpsCounter').innerText = frameCount;
                    frameCount = 0;
                    lastTime = now;
                }

                state.time += 0.03;

                // Clear Canvas
                ctx.fillStyle = '#02040a';
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                const center = { x: canvas.width * 0.5, y: canvas.height * 0.5 };

                if (state.pov === 'external') {
                    drawExternalPOV(ctx, center, state);
                } else {
                    drawPilotPOV(ctx, center, state);
                }

                requestAnimationFrame(animate);
            }

            // --- CANVAS DRAWING FUNCTIONS ---

            // POV 1: EXTERNAL OBSERVER
            function drawExternalPOV(ctx, center, state) {
                // 1. Draw Curved Spacetime Grid
                drawSpacetimeGrid(ctx, center, state);

                // 2. Draw Reference Environment Objects
                drawReferenceObjectsExternal(ctx, center, state);

                // 3. Draw 6D Metric Bubble Around Suit
                const baseSuitRadius = 35;
                // Calculate visual suit radius based on logarithmic scale factor
                // Normal scale exponent is approx 0.25 (1.8m). Micro is -3 (1mm).
                const scaleRatio = Math.pow(10, (state.scaleExponent - 0.25) * 0.5);
                let visualSuitRadius = baseSuitRadius * scaleRatio;
                visualSuitRadius = Math.max(3, Math.min(canvas.height * 0.4, visualSuitRadius));

                // Bubble Glow & Rings
                drawMetricBubble(ctx, center.x, center.y, visualSuitRadius, state);

                // Suit Character (Scaled)
                drawSuitCharacter(ctx, center.x, center.y, visualSuitRadius, state);
            }

            // POV 2: PILOT COCKPIT (INSIDE 1G BUBBLE)
            function drawPilotPOV(ctx, center, state) {
                // 1. Draw Scaling External Universe (Environment zooms in/out)
                drawReferenceObjectsPilotPOV(ctx, center, state);

                // 2. Draw Fixed Cockpit HUD / Suit Interface
                drawCockpitHUD(ctx, center, state);

                // 3. Draw Pilot's Suit Centered in 1:1 scale (Constant 1G)
                drawSuitCharacter(ctx, center.x, center.y + 20, 45, state);

                // SAMS 1G Bubble Ring Overlay
                ctx.strokeStyle = 'rgba(0, 255, 102, 0.4)';
                ctx.lineWidth = 2;
                ctx.setLineDash([8, 8]);
                ctx.beginPath();
                ctx.arc(center.x, center.y + 20, 110, 0, Math.PI * 2);
                ctx.stroke();
                ctx.setLineDash([]);
            }

            // SPACETIME GRID DISTORTION
            function drawSpacetimeGrid(ctx, center, state) {
                ctx.strokeStyle = 'rgba(0, 243, 255, 0.12)';
                ctx.lineWidth = 1;

                const gridSize = 30;
                const rows = Math.ceil(canvas.height / gridSize);
                const cols = Math.ceil(canvas.width / gridSize);

                for (let r = 0; r <= rows; r++) {
                    ctx.beginPath();
                    for (let c = 0; c <= cols; c++) {
                        let x = c * gridSize;
                        let y = r * gridSize;

                        // Calculate distance from 6D Metric Bubble
                        const dx = x - center.x;
                        const dy = y - center.y;
                        const dist = Math.sqrt(dx * dx + dy * dy);

                        if (dist < 220) {
                            const distortionFactor = (1 - dist / 220) * (state.scaleExponent < 0 ? 35 : -25);
                            const angle = Math.atan2(dy, dx);
                            x += Math.cos(angle) * distortionFactor;
                            y += Math.sin(angle) * distortionFactor;
                        }

                        if (c === 0) ctx.moveTo(x, y);
                        else ctx.lineTo(x, y);
                    }
                    ctx.stroke();
                }
            }

            // METRIC BUBBLE EFFECT
            function drawMetricBubble(ctx, x, y, radius, state) {
                const bubbleR = radius * 1.6;

                // Piezoelectric SAMS Radial Gradient
                const bGrad = ctx.createRadialGradient(x, y, radius * 0.5, x, y, bubbleR);
                bGrad.addColorStop(0, 'rgba(0, 243, 255, 0.05)');
                bGrad.addColorStop(0.7, 'rgba(176, 0, 255, 0.2)');
                bGrad.addColorStop(1, 'rgba(0, 243, 255, 0.6)');

                ctx.fillStyle = bGrad;
                ctx.beginPath();
                ctx.arc(x, y, bubbleR, 0, Math.PI * 2);
                ctx.fill();

                // Rotating SROS Laser Beams
                ctx.strokeStyle = '#ffb700';
                ctx.lineWidth = 1.5;
                for (let i = 0; i < 4; i++) {
                    const angle = (i * Math.PI / 2) + state.time * (state.srosFreq / 200);
                    const bx = x + Math.cos(angle) * bubbleR;
                    const by = y + Math.sin(angle) * bubbleR;

                    ctx.beginPath();
                    ctx.moveTo(x, y);
                    ctx.lineTo(bx, by);
                    ctx.stroke();
                }

                // Outer MHD Plasma Ring
                ctx.strokeStyle = '#00f3ff';
                ctx.lineWidth = 2;
                ctx.setLineDash([10, 5]);
                ctx.beginPath();
                ctx.arc(x, y, bubbleR, state.time, state.time + Math.PI * 2);
                ctx.stroke();
                ctx.setLineDash([]);
            }

            // SUIT CHARACTER RENDER
            function drawSuitCharacter(ctx, x, y, radius, state) {
                if (radius < 2) return; // Too small

                ctx.save();
                ctx.translate(x, y);

                const scaleRatio = radius / 35;
                ctx.scale(scaleRatio, scaleRatio);

                // Suit Helmet
                ctx.fillStyle = '#0f172a';
                ctx.strokeStyle = '#00f3ff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(0, -18, 12, 0, Math.PI * 2);
                ctx.fill();
                ctx.stroke();

                // Visor Glow
                ctx.fillStyle = '#00f3ff';
                ctx.beginPath();
                ctx.ellipse(3, -18, 7, 4, 0, 0, Math.PI * 2);
                ctx.fill();

                // Suit Body
                ctx.fillStyle = '#1e293b';
                ctx.strokeStyle = '#b000ff';
                ctx.beginPath();
                ctx.roundRect(-12, -4, 24, 30, 6);
                ctx.fill();
                ctx.stroke();

                // Micro-MHD Cores on Chest
                ctx.fillStyle = '#ffb700';
                ctx.beginPath();
                ctx.arc(0, 5, 4, 0, Math.PI * 2);
                ctx.fill();

                // Limbs
                ctx.strokeStyle = '#64748b';
                ctx.lineWidth = 4;
                // Arms
                ctx.beginPath();
                ctx.moveTo(-12, 2);
                ctx.lineTo(-20, 18);
                ctx.moveTo(12, 2);
                ctx.lineTo(20, 18);
                // Legs
                ctx.moveTo(-6, 26);
                ctx.lineTo(-10, 42);
                ctx.moveTo(6, 26);
                ctx.lineTo(10, 42);
                ctx.stroke();

                ctx.restore();
            }

            // EXTERNAL REFERENCE OBJECTS
            function drawReferenceObjectsExternal(ctx, center, state) {
                // Draw Ant Reference Object if in micro/human scale
                if (state.scaleExponent < 1) {
                    const antX = center.x + 140;
                    const antY = center.y + 20;

                    // Giant Ant relative to shrunk suit
                    ctx.save();
                    ctx.translate(antX, antY);

                    ctx.fillStyle = '#334155';
                    ctx.strokeStyle = '#475569';
                    ctx.lineWidth = 2;

                    // Ant Head, Thorax, Abdomen
                    ctx.beginPath();
                    ctx.arc(-25, 0, 10, 0, Math.PI * 2);
                    ctx.arc(0, 0, 8, 0, Math.PI * 2);
                    ctx.arc(30, 0, 18, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.stroke();

                    // Ant Legs
                    ctx.beginPath();
                    ctx.moveTo(0, 0); ctx.lineTo(-10, -25);
                    ctx.moveTo(0, 0); ctx.lineTo(0, -25);
                    ctx.moveTo(0, 0); ctx.lineTo(10, -25);
                    ctx.moveTo(0, 0); ctx.lineTo(-10, 25);
                    ctx.moveTo(0, 0); ctx.lineTo(0, 25);
                    ctx.moveTo(0, 0); ctx.lineTo(10, 25);
                    ctx.stroke();

                    // Label
                    ctx.fillStyle = '#94a3b8';
                    ctx.font = '10px Rajdhani';
                    ctx.fillText("Formiga Operária (Escala Ref: 2.5mm)", -40, 40);

                    ctx.restore();
                }

                // Draw Hydrogen Atom Reference if Quantum scale
                if (state.scaleExponent <= -6) {
                    const atomX = center.x - 160;
                    const atomY = center.y - 40;

                    ctx.strokeStyle = 'rgba(176, 0, 255, 0.6)';
                    ctx.lineWidth = 1.5;
                    ctx.beginPath();
                    ctx.arc(atomX, atomY, 45, 0, Math.PI * 2);
                    ctx.stroke();

                    // Nucleus
                    ctx.fillStyle = '#ff0055';
                    ctx.beginPath();
                    ctx.arc(atomX, atomY, 6, 0, Math.PI * 2);
                    ctx.fill();

                    // Orbiting Electron
                    const eAngle = state.time * 4;
                    const ex = atomX + Math.cos(eAngle) * 45;
                    const ey = atomY + Math.sin(eAngle) * 45;

                    ctx.fillStyle = '#00f3ff';
                    ctx.beginPath();
                    ctx.arc(ex, ey, 3, 0, Math.PI * 2);
                    ctx.fill();

                    ctx.fillStyle = '#c084fc';
                    ctx.font = '10px Rajdhani';
                    ctx.fillText("Núcleo Atômico (Ref: 0.1nm)", atomX - 40, atomY + 65);
                }
            }

            // PILOT POV REFERENCE OBJECTS (EXPANDING UNIVERSE)
            function drawReferenceObjectsPilotPOV(ctx, center, state) {
                // When suit shrinks (exponent drops), external world expands
                const envScale = Math.pow(10, (0.25 - state.scaleExponent) * 0.4);

                ctx.save();
                ctx.translate(center.x, center.y);
                ctx.scale(envScale, envScale);

                // Draw Lab Table / Room Boundaries
                ctx.strokeStyle = 'rgba(255, 255, 255, 0.15)';
                ctx.lineWidth = 1 / envScale;
                ctx.strokeRect(-300, -200, 600, 400);

                // External Ant expanding
                ctx.fillStyle = 'rgba(51, 65, 85, 0.4)';
                ctx.beginPath();
                ctx.arc(150, 0, 25, 0, Math.PI * 2);
                ctx.fill();

                ctx.restore();
            }

            // COCKPIT HUD FOR PILOT POV
            function drawCockpitHUD(ctx, center, state) {
                // Circular Radar Crosshair
                ctx.strokeStyle = 'rgba(0, 243, 255, 0.3)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.arc(center.x, center.y + 20, 180, 0, Math.PI * 2);
                ctx.stroke();

                // Target Lock Reticle
                ctx.strokeStyle = '#ff0055';
                ctx.lineWidth = 1.5;
                ctx.strokeRect(center.x - 30, center.y - 10, 60, 60);

                // Text Overlay
                ctx.fillStyle = '#00f3ff';
                ctx.font = '11px Orbitron';
                ctx.fillText("SAMS BUBBLE: 1.0G STABLE", center.x - 70, center.y - 140);
                ctx.fillText(`METRIC RATIO: 1:${Math.pow(10, -state.scaleExponent).toFixed(0)}`, center.x - 70, center.y + 190);
            }

            // Initialize UI & Start Loop
            updateUI();
            requestAnimationFrame(animate);
        };
    </script>
</body>
</html>

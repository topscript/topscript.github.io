# topscript.github.io
<!DOCTYPE html>
<html lang="ru" class="scroll-smooth antialiased">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STUDIO ARCHIVE // NOIR & CRÉMA × KINETIC LAB</title>

    <!-- Tailwind CSS Engine -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- Lenis Smooth Scroll (v1.1.18) -->
    <script src="https://unpkg.com/lenis@1.1.18/dist/lenis.min.js"></script>

    <!-- GSAP 3.12 & ScrollTrigger -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>

    <!-- Typography: Bodoni Moda, Syne, Space Mono & Plus Jakarta Sans -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,400..900;1,6..96,400..900&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        bodoni: ['"Bodoni Moda"', 'serif'],
                        syne: ['"Syne"', 'sans-serif'],
                        mono: ['"Space Mono"', 'monospace'],
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                    },
                    colors: {
                        obsidian: '#070708',
                        carbon: '#0E0F12',
                        noir: {
                            gold: '#C8A858',
                            goldHover: '#E0C06F',
                            bone: '#F3EFEA',
                            muted: '#8C857E',
                            border: 'rgba(200, 168, 88, 0.22)'
                        },
                        kinetic: {
                            lime: '#CCFF00',
                            limeMuted: '#A8D400',
                            slate: '#7E889B',
                            border: 'rgba(204, 255, 0, 0.22)'
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Lenis setup */
        html.lenis, html.lenis body {
            height: auto;
        }
        .lenis.lenis-smooth {
            scroll-behavior: auto !important;
        }
        .lenis.lenis-smooth [data-lenis-prevent] {
            overscroll-behavior: contain;
        }
        .lenis.lenis-stopped {
            overflow: hidden;
        }

        body {
            background-color: #070708;
            color: #F3EFEA;
            overflow-x: hidden;
            cursor: default;
        }

        /* SVG Film Grain Noise Texture (Tactile editorial overlay) */
        .film-grain {
            position: fixed;
            inset: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 999;
            opacity: 0.045;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
        }

        /* Architectural Hairline Gridlines */
        .hairline-grid {
            background-image: 
                linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 80px 80px;
        }

        /* Magnetic Inverting Cursor */
        .cursor-point {
            width: 7px;
            height: 7px;
            background-color: #FFFFFF;
            border-radius: 9999px;
            position: fixed;
            pointer-events: none;
            z-index: 10000;
            transform: translate(-50%, -50%);
            mix-blend-mode: difference;
        }
        .cursor-ring {
            width: 42px;
            height: 42px;
            border: 1px solid rgba(255, 255, 255, 0.4);
            border-radius: 9999px;
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 8px;
            font-family: 'Space Mono', monospace;
            letter-spacing: 0.15em;
            color: transparent;
            transition: width 0.3s cubic-bezier(0.16, 1, 0.3, 1), 
                        height 0.3s cubic-bezier(0.16, 1, 0.3, 1), 
                        border-color 0.25s ease, 
                        background-color 0.25s ease,
                        color 0.2s ease;
        }
        body.cursor-active .cursor-ring {
            width: 76px;
            height: 76px;
            border-color: #C8A858;
            background-color: rgba(200, 168, 88, 0.12);
            color: #FFFFFF;
        }
        body.cursor-active-kinetic .cursor-ring {
            width: 76px;
            height: 76px;
            border-color: #CCFF00;
            background-color: rgba(204, 255, 0, 0.12);
            color: #CCFF00;
        }

        /* Continuous Kinetic Marquee */
        @keyframes marqueeScroll {
            0% { transform: translateX(0%); }
            100% { transform: translateX(-50%); }
        }
        .marquee-content {
            display: flex;
            width: 200%;
            animation: marqueeScroll 24s linear infinite;
        }
        .marquee-content:hover {
            animation-play-state: paused;
        }

        /* Editorial Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 4px;
        }
        ::-webkit-scrollbar-track {
            background: #070708;
        }
        ::-webkit-scrollbar-thumb {
            background: #23252B;
        }
    </style>
</head>
<body class="selection:bg-[#CCFF00] selection:text-black">

    <!-- Analog Film Grain -->
    <div class="film-grain"></div>

    <!-- Magnetic Blend-Mode Cursor -->
    <div id="cursor-point" class="cursor-point hidden md:block"></div>
    <div id="cursor-ring" class="cursor-ring hidden md:block"></div>

    <!-- Studio Notification System -->
    <div id="toast-deck" class="fixed bottom-6 right-6 z-[100] flex flex-col gap-3 pointer-events-none"></div>

    <header class="fixed top-6 left-1/2 -translate-x-1/2 z-50 w-[95%] max-w-3xl">
        <nav class="bg-black/80 backdrop-blur-2xl border border-white/10 rounded-full p-2 shadow-[0_25px_60px_rgba(0,0,0,0.95)] flex items-center justify-between">
            
            <!-- Technical Status Tag -->
            <div class="flex items-center gap-3 pl-4 pr-2">
                <span class="relative flex h-2 w-2">
                    <span id="nav-indicator-pulse" class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[#C8A858] opacity-80"></span>
                    <span id="nav-indicator" class="relative inline-flex rounded-full h-2 w-2 bg-[#C8A858]"></span>
                </span>
                <span class="text-[10px] font-mono tracking-[0.25em] text-neutral-400 uppercase hidden sm:inline">ARCHIVE 2026 // VOL. 04</span>
            </div>

            <!-- Conceptual Switcher Buttons -->
            <div class="flex items-center gap-1.5 bg-white/5 p-1 rounded-full border border-white/5">
                <button id="tab-noir" onclick="switchDomain('noir')" class="flex items-center gap-2 px-5 py-2 rounded-full text-xs font-bodoni italic tracking-wide transition-all duration-300 bg-[#C8A858] text-black font-semibold shadow-lg">
                    <span class="font-mono text-[9px] not-italic font-bold">01</span>
                    <span>Noir & Créma</span>
                </button>
                <button id="tab-kinetic" onclick="switchDomain('kinetic')" class="flex items-center gap-2 px-5 py-2 rounded-full text-xs font-syne font-extrabold uppercase tracking-wider text-neutral-400 hover:text-white transition-all duration-300">
                    <span class="font-mono text-[9px] font-bold">02</span>
                    <span>Kinetic Lab</span>
                </button>
            </div>

            <!-- Coordinate / Spec Label -->
            <div class="pr-4 pl-2 hidden md:flex items-center text-[10px] font-mono tracking-[0.2em] text-neutral-500">
                <span id="nav-label">SPECIALTY ATELIER</span>
            </div>
        </nav>
    </header>

    <main id="domain-noir" class="relative z-10 transition-opacity duration-500">
        
        <!-- Hero Section with Bodoni Moda & watermarked_img_16151734725852356379.jpg -->
        <section class="min-h-screen relative pt-36 pb-24 md:pt-44 md:pb-32 border-b border-white/[0.08] hairline-grid flex flex-col justify-between">
            <div class="max-w-7xl mx-auto px-6 w-full grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Left Editorial Headline -->
                <div class="lg:col-span-7 space-y-8">
                    <div class="inline-flex items-center gap-3 px-3.5 py-1.5 rounded-full bg-carbon border border-noir-border text-[10px] font-mono tracking-[0.28em] text-noir-gold uppercase">
                        <span class="w-1.5 h-1.5 rounded-full bg-noir-gold animate-pulse"></span>
                        <span>TERROIR D’ORIGINE · SCANDINAVIAN ROAST ARCHITECTURE</span>
                    </div>

                    <h1 class="font-bodoni text-5xl sm:text-7xl lg:text-[5.75rem] font-normal leading-[0.93] tracking-[-0.04em] text-white">
                        L’Élixir Noir <br>
                        <span class="italic font-light text-noir-gold">& Précision</span> <br>
                        du Grain Pur.
                    </h1>

                    <p class="font-sans text-sm sm:text-base text-noir-muted max-w-xl font-light leading-relaxed">
                        Камерное кофейное ателье чистой нордической обжарки. Мы не маскируем зерно темным ростом: только естественная сладость, кристальный терруар и реминерализованная вода BWT до 70 ppm.
                    </p>

                    <!-- Editorial Actions -->
                    <div class="flex flex-wrap items-center gap-5 pt-2">
                        <a href="#noir-radar-sec" class="px-8 py-4 rounded-full text-xs font-syne font-bold uppercase tracking-[0.2em] bg-noir-gold text-black hover:bg-noir-goldHover transition-all duration-300 shadow-[0_10px_35px_rgba(200,168,88,0.25)] active:scale-95 flex items-center gap-3 group">
                            <span>Карта Дегустации</span>
                            <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-1" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2">
                                <line x1="5" y1="12" x2="19" y2="12"></line>
                                <polyline points="12 5 19 12 12 19"></polyline>
                            </svg>
                        </a>
                        <a href="#noir-v60" class="px-8 py-4 rounded-full text-xs font-mono tracking-widest uppercase border border-white/15 hover:border-noir-gold text-noir-bone transition-all active:scale-95">
                            [ V60 CALCULATOR ]
                        </a>
                    </div>

                    <!-- Telemetry Stats Strip -->
                    <div class="pt-8 border-t border-white/[0.08] grid grid-cols-3 gap-6 font-mono">
                        <div>
                            <div class="font-bodoni text-3xl sm:text-4xl text-noir-gold font-light">91.8</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-noir-muted mt-1">SCA Cup Score</div>
                        </div>
                        <div>
                            <div class="font-bodoni text-3xl sm:text-4xl text-white font-light">70 ppm</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-noir-muted mt-1">BWT Water Profile</div>
                        </div>
                        <div>
                            <div class="font-bodoni text-3xl sm:text-4xl text-white font-light">Giesen</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-noir-muted mt-1">W15A Cast Iron</div>
                        </div>
                    </div>
                </div>

                <div class="lg:col-span-5 relative">
                    <div class="relative rounded-3xl p-3 bg-carbon border border-noir-border shadow-[0_30px_70px_rgba(0,0,0,0.9)] group" data-hover-label="POUR-OVER">
                        <div class="relative rounded-2xl overflow-hidden aspect-[4/5] bg-neutral-900">
                            <!-- Injected Primary Coffee Hero Image -->
                            <img src="watermarked_img_16151734725852356379.jpg" 
                                 alt="NOIR Specialty Coffee Atelier V60 Pour Over Extraction" 
                                 class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-105"
                                 onerror="this.src='https://placehold.co/800x1000/0E0F12/C8A858?text=NOIR+POUR-OVER'">
                            <div class="absolute inset-0 bg-gradient-to-t from-obsidian via-transparent to-black/30"></div>

                            <!-- Floating Editorial Placard -->
                            <div class="absolute bottom-6 left-6 right-6 p-5 rounded-2xl bg-black/85 backdrop-blur-xl border border-white/10 shadow-2xl">
                                <div class="flex items-center justify-between">
                                    <div>
                                        <div class="text-[9px] font-mono uppercase tracking-[0.25em] text-noir-gold">LOT DU MOIS · LOT 01</div>
                                        <div class="font-bodoni text-2xl text-white mt-0.5">Panama Geisha Boquete</div>
                                        <div class="text-[11px] font-mono text-noir-muted mt-0.5">Анаэробный натурал · 1850m</div>
                                    </div>
                                    <div class="font-mono text-xs text-noir-gold font-bold bg-noir-gold/10 border border-noir-gold/30 px-3 py-1.5 rounded-full">
                                        890 ₽
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Infinite Editorial Typography Ticker -->
            <div class="w-full overflow-hidden border-t border-b border-white/[0.08] py-3.5 mt-20 bg-carbon/70">
                <div class="marquee-content font-bodoni text-base tracking-[0.25em] text-noir-gold/70 uppercase">
                    <span class="mx-8">PANAMA GEISHA BOQUETE 1850M</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                    <span class="mx-8">ETHIOPIA BANKO GOTITI NATURAL</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                    <span class="mx-8">COLOMBIA PINK BOURBON ANAEROBIC</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                    <span class="mx-8">GIESEN CAST IRON ROASTING METHOD</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                    <span class="mx-8">PANAMA GEISHA BOQUETE 1850M</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                    <span class="mx-8">ETHIOPIA BANKO GOTITI NATURAL</span>
                    <span class="mx-8 font-mono text-neutral-600">✦</span>
                </div>
            </div>
        </section>

        <section class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Roaster Image Showcase -->
                <div class="lg:col-span-6 relative">
                    <div class="rounded-3xl p-3 bg-carbon border border-white/[0.08] shadow-2xl group" data-hover-label="ROASTERY">
                        <div class="rounded-2xl overflow-hidden aspect-[4/3] relative bg-neutral-900">
                            <!-- Injected Roasting Craft & Beans Image -->
                            <img src="watermarked_img_363440889585343541.jpg" 
                                 alt="Giesen Roasting Machine and Micro-lot Coffee Beans" 
                                 class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-105"
                                 onerror="this.src='https://placehold.co/800x600/0E0F12/C8A858?text=ROASTING+CRAFT'">
                            <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
                            <div class="absolute bottom-5 left-5 font-mono text-xs">
                                <span class="text-noir-gold font-bold tracking-widest text-[10px] uppercase">GIESEN W15A ARCHITECTURE</span>
                                <div class="text-white text-sm font-bodoni italic">7-килограммовые микробэтчи прямого импорта</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Craft Editorial Narrative -->
                <div class="lg:col-span-6 space-y-6">
                    <div class="text-[10px] font-mono tracking-[0.3em] uppercase text-noir-gold">CULTURE DE LA TORRÉFACTION</div>
                    <h2 class="font-bodoni text-4xl sm:text-5xl font-normal text-white leading-tight">
                        Чистота чашки, <br>
                        <span class="italic text-noir-gold font-light">не искаженная</span> дымом.
                    </h2>
                    <p class="font-sans text-sm text-noir-muted leading-relaxed font-light">
                        Каждое зерно проходит оптический спектральный контроль до и после обжарки. Мы фиксируем кривую RoR (Rate of Rise) с точностью до 0.1°C в секунду, чтобы сохранить эфирные кислоты жасмина, бергамота и маракуйи без горьких деструктивных смол.
                    </p>
                    <div class="pt-4 border-t border-white/[0.08] grid grid-cols-2 gap-6 font-mono text-xs">
                        <div class="p-4 rounded-2xl bg-carbon border border-white/5">
                            <span class="text-noir-gold font-bold">14 ДНЕЙ</span>
                            <div class="text-neutral-400 text-[11px] mt-1">Контролируемая дегазация в азотной среде</div>
                        </div>
                        <div class="p-4 rounded-2xl bg-carbon border border-white/5">
                            <span class="text-white font-bold">2.4% TDS</span>
                            <div class="text-neutral-400 text-[11px] mt-1">Оптимальный диапазон рефрактометра VST</div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <section id="noir-radar-sec" class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-6">
                <div>
                    <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-noir-gold">SCA FLAVOR RADAR</span>
                    <h2 class="font-bodoni text-4xl sm:text-5xl font-normal text-white mt-2">Органолептический радар микролотов</h2>
                </div>
                <div class="text-xs font-mono text-noir-muted">
                    НАЖМИТЕ НА ЛОТ ДЛЯ ПЕРЕСТРОЕНИЯ МНОГОУГОЛЬНИКА ВКУСА
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
                
                <!-- Lots Menu Cards -->
                <div class="lg:col-span-6 space-y-4 font-mono text-xs">
                    
                    <!-- Lot 1 Button Card -->
                    <div onclick="selectCoffeeLot('geisha', this)" class="lot-card active cursor-pointer p-6 rounded-3xl bg-carbon border border-noir-gold transition-all duration-300">
                        <div class="flex justify-between items-start">
                            <div>
                                <span class="text-[10px] text-noir-gold uppercase tracking-wider font-bold">PANAMA // BOQUETE</span>
                                <h3 class="font-bodoni text-2xl text-white mt-1">Hacienda La Esmeralda Geisha</h3>
                                <p class="text-[11px] text-noir-muted mt-1 font-sans">Жасмин · Цветок кофе · Масло бергамота · Белый персик</p>
                            </div>
                            <span class="font-bold text-noir-gold text-sm">Q 91.8</span>
                        </div>
                    </div>

                    <!-- Lot 2 Button Card -->
                    <div onclick="selectCoffeeLot('ethiopia', this)" class="lot-card cursor-pointer p-6 rounded-3xl bg-carbon border border-white/10 hover:border-white/20 transition-all duration-300">
                        <div class="flex justify-between items-start">
                            <div>
                                <span class="text-[10px] text-noir-muted uppercase tracking-wider font-bold">ETHIOPIA // SIDAMO</span>
                                <h3 class="font-bodoni text-2xl text-white mt-1">Yirgacheffe Banko Gotiti</h3>
                                <p class="text-[11px] text-noir-muted mt-1 font-sans">Цветы липы · Кумкват · Мелисса · Красный чай</p>
                            </div>
                            <span class="font-bold text-white text-sm">Q 89.5</span>
                        </div>
                    </div>

                    <!-- Lot 3 Button Card -->
                    <div onclick="selectCoffeeLot('bourbon', this)" class="lot-card cursor-pointer p-6 rounded-3xl bg-carbon border border-white/10 hover:border-white/20 transition-all duration-300">
                        <div class="flex justify-between items-start">
                            <div>
                                <span class="text-[10px] text-noir-muted uppercase tracking-wider font-bold">COLOMBIA // HUILA</span>
                                <h3 class="font-bodoni text-2xl text-white mt-1">Pink Bourbon Thermal Shock</h3>
                                <p class="text-[11px] text-noir-muted mt-1 font-sans">Спелая малина · Розовая гуава · Личи · Карамель</p>
                            </div>
                            <span class="font-bold text-white text-sm">Q 90.2</span>
                        </div>
                    </div>

                </div>

                <!-- Radar Canvas Container -->
                <div class="lg:col-span-6 flex flex-col items-center justify-center p-8 bg-carbon rounded-3xl border border-white/[0.08] relative">
                    <span class="absolute top-6 left-6 text-[10px] font-mono tracking-widest text-noir-gold uppercase">RADAR GEOMETRY</span>
                    <canvas id="noir-flavor-canvas" width="460" height="460" class="w-full max-w-[420px] aspect-square"></canvas>
                    <div class="text-center font-mono text-[11px] text-noir-muted mt-2">
                        Органолептическая калибровка лаборатории NOIR
                    </div>
                </div>

            </div>
        </section>

        <section id="noir-v60" class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="max-w-2xl mb-16">
                <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-noir-gold">LABORATOIRE V60</span>
                <h2 class="font-bodoni text-4xl sm:text-5xl font-normal text-white mt-2">Калькулятор и таймер пролива V60</h2>
                <p class="font-sans text-sm text-noir-muted mt-2 font-light">
                    Синтезированный звуковой метроном через Web Audio API фиксирует стадии дегазации и спирального пролива.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
                
                <!-- Calculation Matrix -->
                <div class="lg:col-span-7 bg-carbon rounded-3xl border border-white/[0.08] p-8 space-y-8 font-mono text-xs">
                    <!-- Grams Dose -->
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="text-noir-muted uppercase tracking-wider">Сухой помол Comandante C40:</span>
                            <span id="v60-dose-val" class="text-xl font-bold text-noir-gold">18.0 г</span>
                        </div>
                        <input id="v60-dose-slider" type="range" min="12" max="30" step="0.5" value="18" oninput="runV60Calc()" class="w-full accent-noir-gold cursor-pointer">
                    </div>

                    <!-- Ratio Selection -->
                    <div>
                        <div class="text-noir-muted uppercase tracking-wider mb-3">Коэффициент экстракции</div>
                        <div class="grid grid-cols-3 gap-3">
                            <button onclick="pickRatio(15, this)" class="ratio-btn p-3.5 rounded-2xl border border-white/10 bg-obsidian text-center hover:border-white/20">
                                <div class="font-bold text-white">1:15</div>
                                <div class="text-[9px] text-neutral-500 mt-0.5">Плотный сироп</div>
                            </button>
                            <button onclick="pickRatio(16, this)" class="ratio-btn active p-3.5 rounded-2xl border border-noir-gold bg-noir-gold/10 text-center">
                                <div class="font-bold text-noir-gold">1:16</div>
                                <div class="text-[9px] text-noir-gold mt-0.5">Golden Cup</div>
                            </button>
                            <button onclick="pickRatio(17, this)" class="ratio-btn p-3.5 rounded-2xl border border-white/10 bg-obsidian text-center hover:border-white/20">
                                <div class="font-bold text-white">1:17</div>
                                <div class="text-[9px] text-neutral-500 mt-0.5">Чайное тело</div>
                            </button>
                        </div>
                    </div>

                    <!-- Steps Breakdown -->
                    <div class="space-y-3 pt-3 border-t border-white/[0.08]">
                        <div class="flex justify-between p-3.5 rounded-xl bg-obsidian border border-white/5">
                            <span class="text-neutral-400">1. Блуминг (45 сек):</span>
                            <span id="v60-res-bloom" class="text-white font-bold">54 г воды</span>
                        </div>
                        <div class="flex justify-between p-3.5 rounded-xl bg-obsidian border border-white/5">
                            <span class="text-neutral-400">2. Первый спиральный пролив:</span>
                            <span id="v60-res-p1" class="text-white font-bold">172 г воды</span>
                        </div>
                        <div class="flex justify-between p-3.5 rounded-xl bg-obsidian border border-white/5">
                            <span class="text-neutral-400">3. Общий объем BWT воды:</span>
                            <span id="v60-res-total" class="text-noir-gold font-bold">288 г воды</span>
                        </div>
                    </div>
                </div>

                <!-- Clock Visualizer -->
                <div class="lg:col-span-5 bg-carbon rounded-3xl border border-white/[0.08] p-8 flex flex-col items-center justify-between text-center space-y-6">
                    <span class="text-[10px] font-mono tracking-[0.25em] text-noir-gold uppercase">CHRONOMÈTRE D’EXTRACTION</span>
                    
                    <div class="relative w-52 h-52 flex items-center justify-center">
                        <svg class="w-full h-full -rotate-90" viewBox="0 0 100 100">
                            <circle cx="50" cy="50" r="44" stroke="rgba(255,255,255,0.06)" stroke-width="3" fill="none"/>
                            <circle id="v60-circle-meter" cx="50" cy="50" r="44" stroke="#C8A858" stroke-width="3" fill="none" stroke-dasharray="276.46" stroke-dashoffset="276.46" stroke-linecap="round" class="transition-all duration-300"/>
                        </svg>
                        <div class="absolute inset-0 flex flex-col items-center justify-center font-mono">
                            <span id="v60-timer-display" class="font-bodoni text-5xl font-normal text-white">00:00</span>
                            <span id="v60-timer-stage" class="text-[9px] text-noir-muted uppercase tracking-wider mt-1">ГОТОВ К СТАРТУ</span>
                        </div>
                    </div>

                    <div class="flex items-center gap-3 w-full">
                        <button id="v60-btn-run" onclick="toggleV60Chronometer()" class="flex-1 py-4 rounded-full text-xs font-syne font-bold uppercase tracking-widest bg-noir-gold text-black hover:bg-noir-goldHover transition-all active:scale-95 shadow-[0_10px_30px_rgba(200,168,88,0.2)]">
                            Запустить пролив
                        </button>
                        <button onclick="resetV60Chronometer()" class="px-5 py-4 rounded-full text-xs font-mono border border-white/10 hover:border-white text-neutral-400 hover:text-white transition-all active:scale-95">
                            Сброс
                        </button>
                    </div>
                </div>

            </div>
        </section>

        <!-- Tasting Reservation Panel -->
        <section class="py-32 max-w-7xl mx-auto px-6">
            <div class="bg-carbon rounded-3xl border border-noir-border p-8 lg:p-14 shadow-2xl">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-12">
                    <div class="lg:col-span-6 space-y-6">
                        <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-noir-gold font-bold">RÉSERVATION PRIVÉE</span>
                        <h2 class="font-bodoni text-4xl sm:text-5xl font-normal text-white">Персональный каппинг & бронь столика</h2>
                        <p class="font-sans text-sm text-noir-muted font-light leading-relaxed">
                            Опыт дегустации с шеф-бариста ателье. Разбор терруаров, чистых кислотностей и оценка по протоколу SCA.
                        </p>
                        <div class="space-y-2 pt-2 font-mono text-xs text-neutral-400">
                            <div>✦ Москва, Большая Никитская, 24/1</div>
                            <div>✦ Время каппингов: 11:00 / 16:00 / 19:30</div>
                        </div>
                    </div>

                    <div class="lg:col-span-6">
                        <form onsubmit="handleNoirReservation(event)" class="space-y-4 font-sans text-xs">
                            <div class="grid grid-cols-2 gap-4">
                                <input type="text" placeholder="Имя гостя" required class="w-full px-4 py-3.5 rounded-2xl bg-obsidian border border-white/10 text-white focus:outline-none focus:border-noir-gold">
                                <input type="tel" placeholder="+7 (999) 000-00-00" required class="w-full px-4 py-3.5 rounded-2xl bg-obsidian border border-white/10 text-white focus:outline-none focus:border-noir-gold font-mono">
                            </div>
                            <select class="w-full px-4 py-3.5 rounded-2xl bg-obsidian border border-white/10 text-white focus:outline-none focus:border-noir-gold font-mono">
                                <option>Каппинг микролотов Панама & Эфиопия (2 персоны)</option>
                                <option>Столик в оранжерее с винилом Linn Sondek</option>
                                <option>Индивидуальная дегустация у ростера Giesen</option>
                            </select>
                            <button type="submit" class="w-full py-4 rounded-full text-xs font-syne font-bold uppercase tracking-widest bg-noir-gold text-black hover:bg-noir-goldHover transition-all active:scale-95 shadow-[0_10px_30px_rgba(200,168,88,0.25)]">
                                Забронировать визит
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </section>

        <!-- Noir Footer -->
        <footer class="border-t border-white/[0.08] py-12 text-center text-xs font-mono text-noir-muted">
            <div class="max-w-7xl mx-auto px-6 flex flex-col sm:flex-row items-center justify-between gap-4">
                <span>© 2026 NOIR & CRÉMA SPECIALTY ATELIER. ALL RIGHTS RESERVED.</span>
                <span>DIRECT TRADE · 70 PPM EXTRACTION</span>
            </div>
        </footer>

    </main>

    <main id="domain-kinetic" class="relative z-10 transition-opacity duration-500 hidden">
        
        <!-- Hero Section with Centerlock Wheel watermarked_img_1082273885348443806.jpg -->
        <section class="min-h-screen relative pt-36 pb-24 md:pt-44 md:pb-32 border-b border-white/[0.08] hairline-grid flex flex-col justify-between">
            <div class="max-w-7xl mx-auto px-6 w-full grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Left Brutalist Kinetic Headline -->
                <div class="lg:col-span-7 space-y-8">
                    <div class="inline-flex items-center gap-3 px-3.5 py-1.5 rounded-full bg-carbon border border-kinetic-border text-[10px] font-mono tracking-[0.28em] text-kinetic-lime uppercase">
                        <span class="w-1.5 h-1.5 rounded-full bg-kinetic-lime animate-pulse"></span>
                        <span>HUNTER TCR1 ROBOTIC MOUNT · ROAD FORCE 560KG ROLLER</span>
                    </div>

                    <h1 class="font-syne text-5xl sm:text-7xl lg:text-8xl font-extrabold leading-[0.92] tracking-[-0.05em] uppercase text-white">
                        KINETIC // <br>
                        <span class="text-transparent bg-clip-text bg-gradient-to-r from-kinetic-lime via-white to-kinetic-lime">ZERO BIAS</span> <br>
                        MOTORSPORT.
                    </h1>

                    <p class="font-mono text-xs sm:text-sm text-kinetic-slate max-w-xl leading-relaxed">
                        Хирургическая колесная инженерия для суперкаров и трековых болидов GT3. Бесконтактный робот Hunter TCR1 Revolution полностью исключает касание металла с диском, а лазерный стенд Road Force устраняет силовую неоднородность на скоростях 300+ км/ч.
                    </p>

                    <!-- Tactical Actions -->
                    <div class="flex flex-wrap items-center gap-5 pt-2">
                        <a href="#kinetic-sim" class="px-8 py-4 rounded-xl text-xs font-mono font-bold uppercase tracking-widest bg-kinetic-lime text-black hover:bg-kinetic-limeMuted transition-all duration-300 shadow-[0_10px_35px_rgba(204,255,0,0.3)] active:scale-95 flex items-center gap-3 group">
                            <span>2D Canvas Симулятор</span>
                            <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-1" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                                <circle cx="12" cy="12" r="10"></circle>
                                <polyline points="12 6 12 12 14 14"></polyline>
                            </svg>
                        </a>
                        <a href="#kinetic-config" class="px-8 py-4 rounded-xl text-xs font-mono tracking-widest uppercase border border-white/15 hover:border-kinetic-lime text-white transition-all active:scale-95">
                            [ РАСЧЕТ КОМПЛЕКСА ]
                        </a>
                    </div>

                    <!-- Telemetry Strip -->
                    <div class="pt-8 border-t border-white/[0.08] grid grid-cols-3 gap-6 font-mono">
                        <div>
                            <div class="font-syne text-3xl sm:text-4xl text-kinetic-lime font-extrabold">0.00%</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-kinetic-slate mt-1">Риск касания диска</div>
                        </div>
                        <div>
                            <div class="font-syne text-3xl sm:text-4xl text-white font-extrabold">24 MIN</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-kinetic-slate mt-1">Регламент бокса</div>
                        </div>
                        <div>
                            <div class="font-syne text-3xl sm:text-4xl text-white font-extrabold">600 NM</div>
                            <div class="text-[9px] uppercase tracking-[0.2em] text-kinetic-slate mt-1">Центргайка Hazet</div>
                        </div>
                    </div>
                </div>

                <div class="lg:col-span-5 relative">
                    <div class="relative rounded-3xl p-3 bg-carbon border border-kinetic-border shadow-[0_30px_70px_rgba(0,0,0,0.95)] group" data-hover-label="CENTERLOCK">
                        <div class="relative rounded-2xl overflow-hidden aspect-[4/5] bg-neutral-900">
                            <!-- Injected Centerlock Wheel Hero Image -->
                            <img src="watermarked_img_1082273885348443806.jpg" 
                                 alt="KINETIC Motorsport Centerlock Forged Wheel and Carbon Ceramic Brake" 
                                 class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-105"
                                 onerror="this.src='https://placehold.co/800x1000/0E0F12/CCFF00?text=KINETIC+WHEEL'">
                            <div class="absolute inset-0 bg-gradient-to-t from-obsidian via-transparent to-black/30"></div>

                            <!-- Live Telemetry Card -->
                            <div class="absolute bottom-6 left-6 right-6 p-5 rounded-2xl bg-black/85 backdrop-blur-xl border border-white/10 shadow-2xl">
                                <div class="flex items-center justify-between">
                                    <div>
                                        <div class="text-[9px] font-mono uppercase tracking-[0.25em] text-kinetic-lime">PORSCHE GT3 SPEC</div>
                                        <div class="font-syne text-xl text-white font-bold mt-0.5">Forged Monoblock R21</div>
                                        <div class="text-[11px] font-mono text-kinetic-slate mt-0.5">Michelin Cup 2 R · 325/30 ZR21</div>
                                    </div>
                                    <span class="px-2.5 py-1 rounded bg-kinetic-lime/10 border border-kinetic-lime/30 text-[10px] font-mono text-kinetic-lime font-bold">
                                        CALIBRATED
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Kinetic Cyber Marquee Strip -->
            <div class="w-full overflow-hidden border-t border-b border-white/[0.08] py-3.5 mt-20 bg-carbon/70">
                <div class="marquee-content font-mono text-xs tracking-[0.3em] text-kinetic-lime uppercase">
                    <span class="mx-8">HUNTER TCR1 REVOLUTION TOUCHLESS ROBOTIC MOUNT</span>
                    <span class="mx-8 text-neutral-600">//</span>
                    <span class="mx-8">ROAD FORCE ELITE LASER DIAGNOSTICS</span>
                    <span class="mx-8 text-neutral-600">//</span>
                    <span class="mx-8">MICHELIN PILOT SPORT CUP 2 R MOTORSPORT SPEC</span>
                    <span class="mx-8 text-neutral-600">//</span>
                    <span class="mx-8">CENTERLOCK 600 NM HAZET TORQUE CALIBRATION</span>
                    <span class="mx-8 text-neutral-600">//</span>
                    <span class="mx-8">HUNTER TCR1 REVOLUTION TOUCHLESS ROBOTIC MOUNT</span>
                    <span class="mx-8 text-neutral-600">//</span>
                </div>
            </div>
        </section>

        <section class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                
                <!-- Compound Lab Image Showcase -->
                <div class="lg:col-span-6 relative">
                    <div class="rounded-3xl p-3 bg-carbon border border-white/[0.08] shadow-2xl group" data-hover-label="LAB VAULT">
                        <div class="rounded-2xl overflow-hidden aspect-[4/3] relative bg-neutral-900">
                            <!-- Injected Compound Lab & Tire Storage Image -->
                            <img src="watermarked_img_10118813158099615149.jpg" 
                                 alt="KINETIC Motorsport Compound Lab and Hunter Tire Storage Vault" 
                                 class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-105"
                                 onerror="this.src='https://placehold.co/800x600/0E0F12/CCFF00?text=TIRE+VAULT+LAB'">
                            <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
                            <div class="absolute bottom-5 left-5 font-mono text-xs">
                                <span class="text-kinetic-lime font-bold tracking-widest text-[10px] uppercase">CLIMATE VAULT // +16°C</span>
                                <div class="text-white text-sm font-syne font-bold">Консервация компаунда и балансировочный стенд</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Technical Workflow Description -->
                <div class="lg:col-span-6 space-y-6">
                    <div class="text-[10px] font-mono tracking-[0.3em] uppercase text-kinetic-lime">ENGINEERING PRECISION</div>
                    <h2 class="font-syne text-4xl sm:text-5xl font-extrabold text-white leading-tight uppercase">
                        Лабораторный регламент <br>
                        <span class="text-kinetic-lime">чистого бокса</span>.
                    </h2>
                    <p class="font-mono text-xs sm:text-sm text-kinetic-slate leading-relaxed">
                        Никаких механических монтировок и случайных царапин на полированных ободах. Компьютерный сенсор Hunter TCR1 сканирует профиль диска оптическим лазером, гидравлические ролики аккуратно заводят борт шины, а прижимной барабан Road Force нагружает колесо весом 560 кг для имитации скоростной трассы.
                    </p>
                    <div class="pt-4 border-t border-white/[0.08] grid grid-cols-2 gap-6 font-mono text-xs">
                        <div class="p-4 rounded-2xl bg-carbon border border-white/5">
                            <span class="text-kinetic-lime font-bold">0.5 ГРАММА</span>
                            <div class="text-neutral-400 text-[11px] mt-1">Допуск динамического дисбаланса колеса</div>
                        </div>
                        <div class="p-4 rounded-2xl bg-carbon border border-white/5">
                            <span class="text-white font-bold">99.9% N2</span>
                            <div class="text-neutral-400 text-[11px] mt-1">Осушенный азот исключает скачки PSI</div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <section id="kinetic-sim" class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="flex flex-col lg:flex-row lg:items-end justify-between mb-16 gap-6">
                <div>
                    <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-kinetic-lime">CANVAS MOTORSPORT SIMULATOR</span>
                    <h2 class="font-syne text-3xl sm:text-5xl font-extrabold text-white uppercase mt-2">Физический 2D симулятор колеса</h2>
                    <p class="font-mono text-xs sm:text-sm text-kinetic-slate mt-2 max-w-xl">
                        Потяните колесо курсором или пальцем для инерционного вращения. Меняйте тип кованых спиц, цвет карбон-керамического суппорта и давление PSI.
                    </p>
                </div>

                <div class="flex items-center gap-3">
                    <button id="btn-spin-dyno" onclick="toggleDynoSpin()" class="px-5 py-2.5 rounded-lg text-xs font-mono font-bold tracking-wider uppercase bg-kinetic-lime text-black shadow-[0_5px_20px_rgba(204,255,0,0.3)]">
                        Вращение стенда [RPM]
                    </button>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center bg-carbon rounded-3xl border border-white/[0.08] p-6 lg:p-12">
                
                <!-- Draggable 2D Wheel Canvas -->
                <div class="lg:col-span-7 flex flex-col items-center justify-center relative select-none">
                    <div class="w-full max-w-lg aspect-square relative cursor-grab active:cursor-grabbing">
                        <canvas id="kinetic-wheel-canvas" width="550" height="550" class="w-full h-full rounded-2xl bg-black/50 border border-white/5"></canvas>
                        
                        <div class="absolute top-4 left-4 font-mono text-[10px] text-kinetic-slate space-y-1">
                            <div>ANGULAR VELOCITY: <span id="dyno-rads" class="text-white font-bold">0.0 RAD/S</span></div>
                            <div>TIRE PROFILE: <span class="text-kinetic-lime font-bold">325/30 ZR21</span></div>
                        </div>

                        <div class="absolute bottom-4 right-4 font-mono text-[9px] text-kinetic-slate bg-black/80 px-3 py-1 rounded border border-white/10">
                            DRAG WHEEL TO ROTATE
                        </div>
                    </div>
                </div>

                <!-- Simulator Telemetry Controls -->
                <div class="lg:col-span-5 space-y-6 font-mono text-xs">
                    
                    <!-- Spoke Switcher -->
                    <div>
                        <div class="text-[10px] uppercase tracking-wider text-kinetic-slate mb-3">1. Архитектура кованого диска</div>
                        <div class="grid grid-cols-3 gap-2">
                            <button onclick="setWheelSpokes(5, this)" class="spoke-btn active p-3 rounded-lg border border-kinetic-lime bg-kinetic-lime/10 text-white font-bold">
                                5-Twin Spoke
                            </button>
                            <button onclick="setWheelSpokes(10, this)" class="spoke-btn p-3 rounded-lg border border-white/10 bg-obsidian text-neutral-400 hover:text-white">
                                10-Spoke GT
                            </button>
                            <button onclick="setWheelSpokes(0, this)" class="spoke-btn p-3 rounded-lg border border-white/10 bg-obsidian text-neutral-400 hover:text-white">
                                Turbofan Aero
                            </button>
                        </div>
                    </div>

                    <!-- Caliper Hue -->
                    <div>
                        <div class="text-[10px] uppercase tracking-wider text-kinetic-slate mb-3">2. Карбон-керамический суппорт</div>
                        <div class="flex gap-3">
                            <button onclick="setWheelCaliper('#CCFF00', this)" class="caliper-btn active px-4 py-2 rounded border border-kinetic-lime bg-white/5 text-kinetic-lime font-bold">
                                Acid Lime
                            </button>
                            <button onclick="setWheelCaliper('#E11D48', this)" class="caliper-btn px-4 py-2 rounded border border-white/10 bg-white/5 text-rose-400">
                                Rosso Corsa
                            </button>
                            <button onclick="setWheelCaliper('#C8A858', this)" class="caliper-btn px-4 py-2 rounded border border-white/10 bg-white/5 text-amber-300">
                                Gold Matrix
                            </button>
                        </div>
                    </div>

                    <!-- PSI Deflection Slider -->
                    <div class="p-4 rounded-xl bg-obsidian border border-white/5 space-y-2">
                        <div class="flex justify-between items-center">
                            <span class="text-neutral-400 uppercase text-[10px]">Давление покрышки (деформация борта):</span>
                            <span id="kinetic-psi-val" class="text-white font-bold text-sm">32.0 PSI (2.2 BAR)</span>
                        </div>
                        <input id="kinetic-psi-slider" type="range" min="26" max="44" step="0.5" value="32" oninput="adjustWheelPsi(this.value)" class="w-full accent-kinetic-lime cursor-pointer">
                    </div>

                </div>

            </div>
        </section>

        <section id="kinetic-config" class="py-32 max-w-7xl mx-auto px-6 border-b border-white/[0.08]">
            <div class="max-w-2xl mb-16">
                <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-kinetic-lime">WORKFLOW ESTIMATOR</span>
                <h2 class="font-syne text-3xl sm:text-5xl font-extrabold text-white uppercase mt-2">Конфигуратор комплекса работ</h2>
                <p class="font-mono text-xs sm:text-sm text-kinetic-slate mt-2">
                    Мгновенный расчет стоимости шиномонтажного цикла под ключ с гарантией отсутствия биения на скоростях свыше 300 км/ч.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
                
                <!-- Options Panel -->
                <div class="lg:col-span-8 bg-carbon rounded-3xl border border-white/[0.08] p-8 space-y-8 font-mono text-xs">
                    
                    <!-- Vehicle Chassis -->
                    <div>
                        <div class="text-[10px] uppercase tracking-wider text-kinetic-slate mb-3">Класс шасси автомобиля</div>
                        <div class="grid grid-cols-3 gap-3">
                            <button onclick="pickChassis('gt', this)" class="chassis-btn active p-4 rounded-xl border border-kinetic-lime bg-kinetic-lime/10 text-white font-bold text-left">
                                <div>GT / Спорткар</div>
                                <div class="text-[9px] text-neutral-400 font-normal mt-1">Центргайка, Run-Flat</div>
                            </button>
                            <button onclick="pickChassis('suv', this)" class="chassis-btn p-4 rounded-xl border border-white/10 bg-obsidian text-neutral-400 hover:text-white text-left">
                                <div>Performance SUV</div>
                                <div class="text-[9px] text-neutral-400 font-normal mt-1">Urus, Cayenne, X5M</div>
                            </button>
                            <button onclick="pickChassis('sedan', this)" class="chassis-btn p-4 rounded-xl border border-white/10 bg-obsidian text-neutral-400 hover:text-white text-left">
                                <div>Sport Sedan</div>
                                <div class="text-[9px] text-neutral-400 font-normal mt-1">M5, RS6, Panamera</div>
                            </button>
                        </div>
                    </div>

                    <!-- Rim Radius R18 - R23 -->
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="text-[10px] uppercase tracking-wider text-kinetic-slate">Диаметр обода</span>
                            <span id="label-rim-radius" class="text-kinetic-lime font-bold">РАДИУС R21</span>
                        </div>
                        <div class="grid grid-cols-6 gap-2">
                            <button onclick="pickRimRadius(18, this)" class="rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime">R18</button>
                            <button onclick="pickRimRadius(19, this)" class="rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime">R19</button>
                            <button onclick="pickRimRadius(20, this)" class="rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime">R20</button>
                            <button onclick="pickRimRadius(21, this)" class="rim-btn active py-3 rounded-lg border border-kinetic-lime bg-kinetic-lime text-black font-bold text-center">R21</button>
                            <button onclick="pickRimRadius(22, this)" class="rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime">R22</button>
                            <button onclick="pickRimRadius(23, this)" class="rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime">R23+</button>
                        </div>
                    </div>

                    <!-- Precision Upgrades -->
                    <div>
                        <div class="text-[10px] uppercase tracking-wider text-kinetic-slate mb-3">Высокоточные сервисы Hunter</div>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                            <label class="p-3.5 rounded-xl border border-white/10 bg-obsidian flex items-start gap-3 cursor-pointer hover:border-white/20">
                                <input type="checkbox" id="chk-roadforce" checked onchange="calcKineticSum()" class="mt-1 accent-kinetic-lime">
                                <div>
                                    <div class="font-bold text-white">Hunter Road Force Elite</div>
                                    <div class="text-[9px] text-neutral-400">Устранение бокового увода (+2 600 ₽)</div>
                                </div>
                            </label>
                            <label class="p-3.5 rounded-xl border border-white/10 bg-obsidian flex items-start gap-3 cursor-pointer hover:border-white/20">
                                <input type="checkbox" id="chk-vault" onchange="calcKineticSum()" class="mt-1 accent-kinetic-lime">
                                <div>
                                    <div class="font-bold text-white">Шинный отель Apex Vault</div>
                                    <div class="text-[9px] text-neutral-400">Климат +16°C (сезонное хранение) (+4 500 ₽)</div>
                                </div>
                            </label>
                            <label class="p-3.5 rounded-xl border border-white/10 bg-obsidian flex items-start gap-3 cursor-pointer hover:border-white/20">
                                <input type="checkbox" id="chk-nitro" checked onchange="calcKineticSum()" class="mt-1 accent-kinetic-lime">
                                <div>
                                    <div class="font-bold text-white">Накачка Азотом 99.9%</div>
                                    <div class="text-[9px] text-neutral-400">Стабильность давления на треке (+1 000 ₽)</div>
                                </div>
                            </label>
                            <label class="p-3.5 rounded-xl border border-white/10 bg-obsidian flex items-start gap-3 cursor-pointer hover:border-white/20">
                                <input type="checkbox" id="chk-wash" checked onchange="calcKineticSum()" class="mt-1 accent-kinetic-lime">
                                <div>
                                    <div class="font-bold text-white">Ультразвуковая мойка</div>
                                    <div class="text-[9px] text-neutral-400">Снятие тормозной пыли с полок обода (+1 200 ₽)</div>
                                </div>
                            </label>
                        </div>
                    </div>

                </div>

                <!-- Rolling Price Summary -->
                <div class="lg:col-span-4 bg-carbon rounded-3xl border border-kinetic-lime/30 p-8 space-y-6 font-mono sticky top-28 shadow-2xl">
                    <div class="flex justify-between items-center border-b border-white/10 pb-4 text-xs">
                        <span class="text-kinetic-slate uppercase">Калькуляция</span>
                        <span class="px-2 py-0.5 rounded bg-kinetic-lime/10 text-kinetic-lime text-[10px] font-bold">4 КОЛЕСА ПОД КЛЮЧ</span>
                    </div>

                    <div>
                        <div class="text-4xl sm:text-5xl font-extrabold text-white flex items-baseline gap-2 font-syne">
                            <span id="kinetic-sum-roll">10 100</span>
                            <span class="text-kinetic-lime text-2xl font-mono">₽</span>
                        </div>
                        <div class="text-[11px] text-kinetic-slate mt-2">
                            Время выполнения: <span class="text-white font-bold">~25-30 минут</span>
                        </div>
                    </div>

                    <div class="space-y-2 pt-2 border-t border-white/10 text-xs">
                        <div class="flex justify-between text-neutral-400">
                            <span>Базовый робот-монтаж:</span>
                            <span id="sub-base" class="text-white font-bold">5 300 ₽</span>
                        </div>
                        <div class="flex justify-between text-neutral-400">
                            <span>Опции Hunter:</span>
                            <span id="sub-addons" class="text-white font-bold">4 800 ₽</span>
                        </div>
                    </div>

                    <button onclick="bookKineticBay()" class="w-full py-4 rounded-xl text-xs font-bold uppercase tracking-widest bg-kinetic-lime text-black hover:bg-kinetic-limeMuted transition-all shadow-[0_10px_30px_rgba(204,255,0,0.25)] active:scale-95">
                        Забронировать бокс онлайн
                    </button>
                </div>

            </div>
        </section>

        <!-- Kinetic Footer -->
        <footer class="border-t border-white/[0.08] py-12 text-center text-xs font-mono text-kinetic-slate">
            <div class="max-w-7xl mx-auto px-6 flex flex-col sm:flex-row items-center justify-between gap-4">
                <span>© 2026 KINETIC MOTORSPORT ENGINEERING LAB. HUNTER CERTIFIED.</span>
                <span>TOLERANCE 0.5G · ZERO BIAS SPEC</span>
            </div>
        </footer>

    </main>

    <script>
        /* ========================================================================= */
        /* 1. LENIS SMOOTH SCROLL & GSAP TICKER LINKAGE                              */
        /* ========================================================================= */
        let lenisInstance;
        try {
            lenisInstance = new Lenis({
                duration: 1.2,
                easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
                smoothWheel: true,
                touchMultiplier: 1.4,
            });

            lenisInstance.on('scroll', ScrollTrigger.update);

            gsap.ticker.add((time) => {
                lenisInstance.raf(time * 1000);
            });

            gsap.ticker.lagSmoothing(0);
        } catch (err) {
            console.warn('Smooth scroll initiated with browser fallback:', err);
        }

        /* ========================================================================= */
        /* 2. SYNTHESIZED WEB AUDIO ENGINE (ZERO EXTERNAL ASSETS)                    */
        /* ========================================================================= */
        function synthesizeAcousticPulse(freq = 880, dur = 0.08, type = 'sine') {
            try {
                const AudioCtx = window.AudioContext || window.webkitAudioContext;
                if (!AudioCtx) return;
                const ctx = new AudioCtx();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();

                osc.type = type;
                osc.frequency.setValueAtTime(freq, ctx.currentTime);

                gain.gain.setValueAtTime(0.04, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + dur);

                osc.connect(gain);
                gain.connect(ctx.destination);

                osc.start();
                osc.stop(ctx.currentTime + dur);
            } catch (e) {}
        }

        /* ========================================================================= */
        /* 3. MAGNETIC DUAL CURSOR                                                   */
        /* ========================================================================= */
        const cursorPoint = document.getElementById('cursor-point');
        const cursorRing = document.getElementById('cursor-ring');
        let mouseX = -100, mouseY = -100;
        let ringX = -100, ringY = -100;
        let currentDomain = 'noir';

        window.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            if (cursorPoint) {
                cursorPoint.style.left = `${mouseX}px`;
                cursorPoint.style.top = `${mouseY}px`;
            }
        });

        function animateCursorRing() {
            ringX += (mouseX - ringX) * 0.18;
            ringY += (mouseY - ringY) * 0.18;
            if (cursorRing) {
                cursorRing.style.left = `${ringX}px`;
                cursorRing.style.top = `${ringY}px`;
            }
            requestAnimationFrame(animateCursorRing);
        }
        animateCursorRing();

        document.querySelectorAll('[data-hover-label]').forEach(item => {
            item.addEventListener('mouseenter', () => {
                const tag = item.getAttribute('data-hover-label');
                cursorRing.innerText = tag;
                if (currentDomain === 'noir') {
                    document.body.classList.add('cursor-active');
                } else {
                    document.body.classList.add('cursor-active-kinetic');
                }
            });
            item.addEventListener('mouseleave', () => {
                cursorRing.innerText = '';
                document.body.classList.remove('cursor-active', 'cursor-active-kinetic');
            });
        });

        /* ========================================================================= */
        /* 4. TOAST NOTIFICATION HANDLER                                             */
        /* ========================================================================= */
        function fireToast(title, msg, isGold = true) {
            synthesizeAcousticPulse(isGold ? 880 : 1080, 0.09);
            const deck = document.getElementById('toast-deck');
            const card = document.createElement('div');
            
            const accent = isGold ? '#C8A858' : '#CCFF00';
            const borderCol = isGold ? 'border-[#C8A858]/30' : 'border-[#CCFF00]/30';

            card.className = `pointer-events-auto flex items-start gap-3 p-4 rounded-2xl border ${borderCol} bg-[#0E0F12] shadow-2xl max-w-sm transition-all duration-300 transform translate-y-3 opacity-0 text-white`;
            card.innerHTML = `
                <div class="mt-0.5" style="color: ${accent}">
                    <svg class="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2">
                        <polyline points="20 6 9 17 4 12"></polyline>
                    </svg>
                </div>
                <div class="flex-1 font-mono">
                    <div class="text-xs font-bold">${title}</div>
                    <div class="text-[11px] text-neutral-400 mt-0.5 leading-snug">${msg}</div>
                </div>
            `;

            deck.appendChild(card);
            requestAnimationFrame(() => {
                card.classList.remove('translate-y-3', 'opacity-0');
            });

            setTimeout(() => {
                card.classList.add('opacity-0', 'translate-x-4');
                setTimeout(() => card.remove(), 300);
            }, 3800);
        }

        /* ========================================================================= */
        /* 5. DOMAIN SWITCHER (NOIR × KINETIC)                                       */
        /* ========================================================================= */
        function switchDomain(target) {
            synthesizeAcousticPulse(600, 0.05);
            currentDomain = target;

            const domainNoir = document.getElementById('domain-noir');
            const domainKinetic = document.getElementById('domain-kinetic');
            const tabNoir = document.getElementById('tab-noir');
            const tabKinetic = document.getElementById('tab-kinetic');
            const pulse = document.getElementById('nav-indicator-pulse');
            const dot = document.getElementById('nav-indicator');
            const label = document.getElementById('nav-label');

            document.body.classList.remove('cursor-active', 'cursor-active-kinetic');

            if (target === 'noir') {
                domainNoir.classList.remove('hidden');
                domainKinetic.classList.add('hidden');

                tabNoir.className = "flex items-center gap-2 px-5 py-2 rounded-full text-xs font-bodoni italic tracking-wide transition-all duration-300 bg-[#C8A858] text-black font-semibold shadow-lg";
                tabKinetic.className = "flex items-center gap-2 px-5 py-2 rounded-full text-xs font-syne font-extrabold uppercase tracking-wider text-neutral-400 hover:text-white transition-all duration-300";

                pulse.className = "animate-ping absolute inline-flex h-full w-full rounded-full bg-[#C8A858] opacity-80";
                dot.className = "relative inline-flex rounded-full h-2 w-2 bg-[#C8A858]";
                label.innerText = "SPECIALTY ATELIER";
            } else {
                domainNoir.classList.add('hidden');
                domainKinetic.classList.remove('hidden');

                tabKinetic.className = "flex items-center gap-2 px-5 py-2 rounded-full text-xs font-syne font-extrabold uppercase tracking-wider transition-all duration-300 bg-kinetic-lime text-black shadow-lg";
                tabNoir.className = "flex items-center gap-2 px-5 py-2 rounded-full text-xs font-bodoni italic tracking-wide text-neutral-400 hover:text-white transition-all duration-300";

                pulse.className = "animate-ping absolute inline-flex h-full w-full rounded-full bg-[#CCFF00] opacity-80";
                dot.className = "relative inline-flex rounded-full h-2 w-2 bg-[#CCFF00]";
                label.innerText = "APEX MOTORSPORT";

                renderKineticWheel();
            }

            if (lenisInstance) lenisInstance.scrollTo(0, { immediate: true });
            else window.scrollTo(0, 0);

            ScrollTrigger.refresh();
        }

        /* ========================================================================= */
        /* 6. NOIR: INTERACTIVE SCA FLAVOR RADAR (CANVAS)                            */
        /* ========================================================================= */
        const radarCanvas = document.getElementById('noir-flavor-canvas');
        const radarCtx = radarCanvas.getContext('2d');

        const lotProfiles = {
            geisha:   { floral: 9.8, fruit: 9.6, sweet: 9.2, acid: 9.4, body: 7.2 },
            ethiopia: { floral: 9.2, fruit: 8.8, sweet: 8.5, acid: 9.5, body: 7.0 },
            bourbon:  { floral: 7.5, fruit: 9.8, sweet: 9.6, acid: 8.8, body: 8.8 }
        };

        let currentRadarValues = { floral: 9.8, fruit: 9.6, sweet: 9.2, acid: 9.4, body: 7.2 };
        let targetRadarValues = { ...currentRadarValues };

        function drawFlavorRadar() {
            radarCtx.clearRect(0, 0, 460, 460);
            const cx = 230, cy = 230, radius = 150;
            const axes = [
                { name: 'FLORAL / ЦВЕТЫ', key: 'floral' },
                { name: 'FRUIT / ТРОПИКИ', key: 'fruit' },
                { name: 'SWEET / СЛАДОСТЬ', key: 'sweet' },
                { name: 'ACID / КИСЛОТНОСТЬ', key: 'acid' },
                { name: 'BODY / ТЕЛО', key: 'body' }
            ];
            const count = axes.length;

            // Interpolate values toward target
            for (let k in currentRadarValues) {
                currentRadarValues[k] += (targetRadarValues[k] - currentRadarValues[k]) * 0.1;
            }

            // Radar concentric rings
            for (let step = 1; step <= 4; step++) {
                const r = (radius / 4) * step;
                radarCtx.beginPath();
                for (let i = 0; i < count; i++) {
                    const angle = (i * 2 * Math.PI / count) - (Math.PI / 2);
                    const x = cx + Math.cos(angle) * r;
                    const y = cy + Math.sin(angle) * r;
                    if (i === 0) radarCtx.moveTo(x, y);
                    else radarCtx.lineTo(x, y);
                }
                radarCtx.closePath();
                radarCtx.strokeStyle = 'rgba(255, 255, 255, 0.08)';
                radarCtx.lineWidth = 1;
                radarCtx.stroke();
            }

            // Radar Spokes & Labels
            radarCtx.font = '9px "Space Mono", monospace';
            radarCtx.fillStyle = '#8C857E';
            radarCtx.textAlign = 'center';

            axes.forEach((axis, i) => {
                const angle = (i * 2 * Math.PI / count) - (Math.PI / 2);
                const x = cx + Math.cos(angle) * radius;
                const y = cy + Math.sin(angle) * radius;

                radarCtx.beginPath();
                radarCtx.moveTo(cx, cy);
                radarCtx.lineTo(x, y);
                radarCtx.strokeStyle = 'rgba(255, 255, 255, 0.1)';
                radarCtx.stroke();

                // Axis Label
                const labelX = cx + Math.cos(angle) * (radius + 28);
                const labelY = cy + Math.sin(angle) * (radius + 28);
                radarCtx.fillText(axis.name, labelX, labelY);
            });

            // Draw Value Polygon
            radarCtx.beginPath();
            axes.forEach((axis, i) => {
                const angle = (i * 2 * Math.PI / count) - (Math.PI / 2);
                const valNorm = (currentRadarValues[axis.key] - 5) / 5; // map 5-10 to 0-1
                const valR = radius * Math.max(0.2, valNorm);
                const x = cx + Math.cos(angle) * valR;
                const y = cy + Math.sin(angle) * valR;

                if (i === 0) radarCtx.moveTo(x, y);
                else radarCtx.lineTo(x, y);
            });
            radarCtx.closePath();
            radarCtx.fillStyle = 'rgba(200, 168, 88, 0.24)';
            radarCtx.fill();
            radarCtx.strokeStyle = '#C8A858';
            radarCtx.lineWidth = 2;
            radarCtx.stroke();

            // Vertex dots
            axes.forEach((axis, i) => {
                const angle = (i * 2 * Math.PI / count) - (Math.PI / 2);
                const valNorm = (currentRadarValues[axis.key] - 5) / 5;
                const valR = radius * Math.max(0.2, valNorm);
                const x = cx + Math.cos(angle) * valR;
                const y = cy + Math.sin(angle) * valR;

                radarCtx.beginPath();
                radarCtx.arc(x, y, 4, 0, Math.PI * 2);
                radarCtx.fillStyle = '#FFFFFF';
                radarCtx.fill();
            });

            requestAnimationFrame(drawFlavorRadar);
        }
        drawFlavorRadar();

        function selectCoffeeLot(key, el) {
            synthesizeAcousticPulse(720, 0.05);
            targetRadarValues = lotProfiles[key];
            document.querySelectorAll('.lot-card').forEach(c => {
                c.className = "lot-card cursor-pointer p-6 rounded-3xl bg-carbon border border-white/10 hover:border-white/20 transition-all duration-300";
            });
            el.className = "lot-card active cursor-pointer p-6 rounded-3xl bg-carbon border border-noir-gold transition-all duration-300";
        }

        /* ========================================================================= */
        /* 7. NOIR: V60 CALCULATOR & WEB AUDIO CHRONOMETER                           */
        /* ========================================================================= */
        let v60Grams = 18.0;
        let v60RatioCoeff = 16;
        let v60Seconds = 0;
        let v60TimerRef = null;
        let isV60Ticking = false;

        function pickRatio(val, btn) {
            synthesizeAcousticPulse(750, 0.04);
            v60RatioCoeff = val;
            document.querySelectorAll('.ratio-btn').forEach(b => {
                b.className = "ratio-btn p-3.5 rounded-2xl border border-white/10 bg-obsidian text-center hover:border-white/20";
                b.querySelector('div:first-child').className = "font-bold text-white";
                b.querySelector('div:last-child').className = "text-[9px] text-neutral-500 mt-0.5";
            });
            btn.className = "ratio-btn active p-3.5 rounded-2xl border border-noir-gold bg-noir-gold/10 text-center";
            btn.querySelector('div:first-child').className = "font-bold text-noir-gold";
            btn.querySelector('div:last-child').className = "text-[9px] text-noir-gold mt-0.5";
            runV60Calc();
        }

        function runV60Calc() {
            const input = document.getElementById('v60-dose-slider');
            v60Grams = parseFloat(input.value);
            document.getElementById('v60-dose-val').innerText = `${v60Grams.toFixed(1)} г`;

            const waterTotal = Math.round(v60Grams * v60RatioCoeff);
            const waterBloom = Math.round(v60Grams * 3);
            const waterP1 = Math.round(waterTotal * 0.6);

            document.getElementById('v60-res-bloom').innerText = `${waterBloom} г воды`;
            document.getElementById('v60-res-p1').innerText = `${waterP1} г воды`;
            document.getElementById('v60-res-total').innerText = `${waterTotal} г воды`;
        }

        function toggleV60Chronometer() {
            const btn = document.getElementById('v60-btn-run');
            if (!isV60Ticking) {
                isV60Ticking = true;
                btn.innerText = 'Пауза пролива';
                synthesizeAcousticPulse(880, 0.1);

                v60TimerRef = setInterval(() => {
                    v60Seconds++;
                    refreshV60ClockDisplay();
                    if (v60Seconds % 30 === 0) synthesizeAcousticPulse(1100, 0.08);
                }, 1000);
            } else {
                isV60Ticking = false;
                btn.innerText = 'Продолжить';
                clearInterval(v60TimerRef);
                synthesizeAcousticPulse(440, 0.08);
            }
        }

        function resetV60Chronometer() {
            isV60Ticking = false;
            clearInterval(v60TimerRef);
            v60Seconds = 0;
            document.getElementById('v60-btn-run').innerText = 'Запустить пролив';
            refreshV60ClockDisplay();
        }

        function refreshV60ClockDisplay() {
            const m = Math.floor(v60Seconds / 60);
            const s = v60Seconds % 60;
            document.getElementById('v60-timer-display').innerText = 
                `${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;

            const stage = document.getElementById('v60-timer-stage');
            if (v60Seconds === 0) stage.innerText = 'ГОТОВ К СТАРТУ';
            else if (v60Seconds <= 45) stage.innerText = 'ФАЗА 1: ДЕГАЗАЦИЯ (БЛУМИНГ)';
            else if (v60Seconds <= 90) stage.innerText = 'ФАЗА 2: СПИРАЛЬНЫЙ ПРОЛИВ';
            else if (v60Seconds <= 150) stage.innerText = 'ФАЗА 3: ЦЕНТРАЛЬНЫЙ ПРОЛИВ';
            else stage.innerText = 'ФИНИШ: ДРОП-ДАУН ФИЛЬТРАЦИИ';

            const circ = 276.46;
            const prog = Math.min(v60Seconds / 180, 1);
            document.getElementById('v60-circle-meter').style.strokeDashoffset = circ - (circ * prog);
        }

        function handleNoirReservation(e) {
            e.preventDefault();
            fireToast('Столик подтвержден', 'Ваш дегустационный визит в NOIR & CRÉMA успешно внесен в журнал.', true);
            e.target.reset();
        }

        /* ========================================================================= */
        /* 8. KINETIC: PROCEDURAL 2D WHEEL CANVAS PHYSICS                            */
        /* ========================================================================= */
        const wheelCanvas = document.getElementById('kinetic-wheel-canvas');
        const wheelCtx = wheelCanvas.getContext('2d');

        let wheelAngle = 0;
        let wheelVel = 0;
        let isDynoActive = false;
        let wheelSpokeType = 5;
        let wheelCaliperColor = '#CCFF00';
        let currentPsi = 32.0;

        let isWheelDragging = false;
        let touchStartCoordX = 0;

        wheelCanvas.addEventListener('mousedown', (e) => {
            isWheelDragging = true;
            touchStartCoordX = e.clientX;
        });
        window.addEventListener('mouseup', () => { isWheelDragging = false; });
        window.addEventListener('mousemove', (e) => {
            if (isWheelDragging) {
                const dx = e.clientX - touchStartCoordX;
                wheelVel = dx * 0.005;
                wheelAngle += wheelVel;
                touchStartCoordX = e.clientX;
            }
        });

        wheelCanvas.addEventListener('touchstart', (e) => {
            isWheelDragging = true;
            touchStartCoordX = e.touches[0].clientX;
        });
        window.addEventListener('touchend', () => { isWheelDragging = false; });
        wheelCanvas.addEventListener('touchmove', (e) => {
            if (isWheelDragging && e.touches.length > 0) {
                const dx = e.touches[0].clientX - touchStartCoordX;
                wheelVel = dx * 0.005;
                wheelAngle += wheelVel;
                touchStartCoordX = e.touches[0].clientX;
            }
        });

        function toggleDynoSpin() {
            isDynoActive = !isDynoActive;
            const btn = document.getElementById('btn-spin-dyno');
            if (isDynoActive) {
                btn.innerText = 'Остановить Dyno';
                synthesizeAcousticPulse(960, 0.08);
            } else {
                btn.innerText = 'Вращение стенда [RPM]';
                synthesizeAcousticPulse(480, 0.08);
            }
        }

        function setWheelSpokes(spokes, btn) {
            synthesizeAcousticPulse(700, 0.04);
            wheelSpokeType = spokes;
            document.querySelectorAll('.spoke-btn').forEach(b => {
                b.className = "spoke-btn p-3 rounded-lg border border-white/10 bg-obsidian text-neutral-400 hover:text-white";
            });
            btn.className = "spoke-btn active p-3 rounded-lg border border-kinetic-lime bg-kinetic-lime/10 text-white font-bold";
        }

        function setWheelCaliper(color, btn) {
            synthesizeAcousticPulse(700, 0.04);
            wheelCaliperColor = color;
            document.querySelectorAll('.caliper-btn').forEach(b => {
                b.classList.remove('border-kinetic-lime', 'font-bold');
                b.classList.add('border-white/10');
            });
            btn.classList.remove('border-white/10');
            btn.classList.add('border-kinetic-lime', 'font-bold');
        }

        function adjustWheelPsi(val) {
            currentPsi = parseFloat(val);
            const bar = (currentPsi * 0.0689476).toFixed(1);
            document.getElementById('kinetic-psi-val').innerText = `${currentPsi.toFixed(1)} PSI (${bar} BAR)`;
        }

        function renderKineticWheel() {
            wheelCtx.clearRect(0, 0, 550, 550);
            const cx = 275, cy = 275;

            if (isDynoActive) {
                wheelVel = 0.07;
            } else if (!isWheelDragging) {
                wheelVel *= 0.965;
            }
            wheelAngle += wheelVel;

            const rads = (Math.abs(wheelVel) * 60).toFixed(1);
            const hud = document.getElementById('dyno-rads');
            if (hud) hud.innerText = `${rads} RAD/S`;

            const tireR = 244;
            const rimR = 175;
            const psiDeflection = (36 - currentPsi) * 0.38;

            wheelCtx.save();
            wheelCtx.translate(cx, cy);

            // Tire Rubber Tread
            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, tireR + psiDeflection, 0, Math.PI * 2);
            wheelCtx.fillStyle = '#0F1115';
            wheelCtx.fill();
            wheelCtx.strokeStyle = '#1C2028';
            wheelCtx.lineWidth = 14;
            wheelCtx.stroke();

            // Tread Sipes
            for (let i = 0; i < 36; i++) {
                const a = (i * Math.PI / 18) + wheelAngle;
                const x1 = Math.cos(a) * (tireR - 4);
                const y1 = Math.sin(a) * (tireR - 4);
                const x2 = Math.cos(a) * (tireR + 8);
                const y2 = Math.sin(a) * (tireR + 8);

                wheelCtx.beginPath();
                wheelCtx.moveTo(x1, y1);
                wheelCtx.lineTo(x2, y2);
                wheelCtx.strokeStyle = 'rgba(0,0,0,0.8)';
                wheelCtx.lineWidth = 3;
                wheelCtx.stroke();
            }

            // Sidewall Branding
            wheelCtx.save();
            wheelCtx.rotate(wheelAngle);
            wheelCtx.font = 'bold 9px "Space Mono", monospace';
            wheelCtx.fillStyle = 'rgba(255, 255, 255, 0.45)';
            wheelCtx.textAlign = 'center';
            wheelCtx.fillText('MICHELIN PILOT SPORT CUP 2 R', 0, -205);
            wheelCtx.fillStyle = '#CCFF00';
            wheelCtx.fillText(`325/30 ZR21 · ULTRA TRACK · ${currentPsi.toFixed(1)} PSI`, 0, 215);
            wheelCtx.restore();

            // Carbon Ceramic Rotor (Stationary)
            const rotorR = 136;
            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, rotorR, 0, Math.PI * 2);
            wheelCtx.fillStyle = '#1C1E24';
            wheelCtx.fill();
            wheelCtx.strokeStyle = '#2E323D';
            wheelCtx.lineWidth = 2;
            wheelCtx.stroke();

            // Perforated Rotor Holes
            for (let r = 85; r < 125; r += 14) {
                const holes = Math.floor(r * 0.35);
                for (let h = 0; h < holes; h++) {
                    const hAngle = (h * (Math.PI * 2 / holes)) + (wheelAngle * 0.1);
                    const hx = Math.cos(hAngle) * r;
                    const hy = Math.sin(hAngle) * r;
                    wheelCtx.beginPath();
                    wheelCtx.arc(hx, hy, 1.8, 0, Math.PI * 2);
                    wheelCtx.fillStyle = '#08080A';
                    wheelCtx.fill();
                }
            }

            // Motorsport Caliper
            wheelCtx.save();
            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, rotorR + 6, -Math.PI * 0.85, -Math.PI * 0.35);
            wheelCtx.arc(0, 0, rotorR - 38, -Math.PI * 0.35, -Math.PI * 0.85, true);
            wheelCtx.closePath();
            wheelCtx.fillStyle = wheelCaliperColor;
            wheelCtx.fill();
            wheelCtx.strokeStyle = 'rgba(0,0,0,0.5)';
            wheelCtx.lineWidth = 3;
            wheelCtx.stroke();

            wheelCtx.rotate(-Math.PI * 0.6);
            wheelCtx.font = 'bold 9px "Syne", sans-serif';
            wheelCtx.fillStyle = '#000000';
            wheelCtx.textAlign = 'center';
            wheelCtx.fillText('KINETIC · CERAMIC', 0, -118);
            wheelCtx.restore();

            // Rotating Forged Spokes
            wheelCtx.save();
            wheelCtx.rotate(wheelAngle);

            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, rimR, 0, Math.PI * 2);
            wheelCtx.strokeStyle = '#484F60';
            wheelCtx.lineWidth = 6;
            wheelCtx.stroke();

            if (wheelSpokeType === 5) {
                for (let s = 0; s < 5; s++) {
                    const sa = s * (Math.PI * 2 / 5);
                    wheelCtx.save();
                    wheelCtx.rotate(sa);

                    wheelCtx.beginPath();
                    wheelCtx.moveTo(-16, 25);
                    wheelCtx.lineTo(-8, rimR - 5);
                    wheelCtx.lineTo(-1, rimR - 5);
                    wheelCtx.lineTo(-6, 25);
                    wheelCtx.closePath();
                    wheelCtx.fillStyle = '#838B9C';
                    wheelCtx.fill();

                    wheelCtx.beginPath();
                    wheelCtx.moveTo(6, 25);
                    wheelCtx.lineTo(1, rimR - 5);
                    wheelCtx.lineTo(8, rimR - 5);
                    wheelCtx.lineTo(16, 25);
                    wheelCtx.closePath();
                    wheelCtx.fillStyle = '#5A6273';
                    wheelCtx.fill();

                    wheelCtx.restore();
                }
            } else if (wheelSpokeType === 10) {
                for (let s = 0; s < 10; s++) {
                    const sa = s * (Math.PI * 2 / 10);
                    wheelCtx.save();
                    wheelCtx.rotate(sa);
                    wheelCtx.beginPath();
                    wheelCtx.moveTo(-6, 25);
                    wheelCtx.lineTo(-3, rimR - 5);
                    wheelCtx.lineTo(3, rimR - 5);
                    wheelCtx.lineTo(6, 25);
                    wheelCtx.closePath();
                    wheelCtx.fillStyle = (s % 2 === 0) ? '#9BA3B5' : '#60687A';
                    wheelCtx.fill();
                    wheelCtx.restore();
                }
            } else {
                // Turbofan Aero
                wheelCtx.beginPath();
                wheelCtx.arc(0, 0, rimR - 4, 0, Math.PI * 2);
                wheelCtx.fillStyle = 'rgba(16, 19, 26, 0.9)';
                wheelCtx.fill();
                wheelCtx.strokeStyle = '#CCFF00';
                wheelCtx.lineWidth = 2;
                wheelCtx.stroke();

                for (let a = 0; a < 6; a++) {
                    const aa = a * (Math.PI * 2 / 6);
                    wheelCtx.save();
                    wheelCtx.rotate(aa);
                    wheelCtx.fillStyle = '#CCFF00';
                    wheelCtx.fillRect(45, -2, 70, 4);
                    wheelCtx.restore();
                }
            }

            // Centerlock Hub
            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, 32, 0, Math.PI * 2);
            wheelCtx.fillStyle = '#0D1017';
            wheelCtx.fill();
            wheelCtx.strokeStyle = '#CCFF00';
            wheelCtx.lineWidth = 3;
            wheelCtx.stroke();

            wheelCtx.beginPath();
            wheelCtx.arc(0, 0, 16, 0, Math.PI * 2);
            wheelCtx.fillStyle = '#CCFF00';
            wheelCtx.fill();

            wheelCtx.restore();
            wheelCtx.restore();

            requestAnimationFrame(renderKineticWheel);
        }
        renderKineticWheel();

        /* ========================================================================= */
        /* 9. KINETIC: DYNAMIC PRICE ESTIMATOR                                       */
        /* ========================================================================= */
        let pickedChassis = 'gt';
        let pickedRadius = 21;
        let animatedTotalSum = 10100;

        const radiusPriceTable = {
            18: 3600,
            19: 4100,
            20: 4700,
            21: 5300,
            22: 6300,
            23: 7400
        };

        const chassisMultiplier = {
            gt: 1.25,
            suv: 1.20,
            sedan: 1.00
        };

        function pickChassis(type, btn) {
            synthesizeAcousticPulse(680, 0.04);
            pickedChassis = type;
            document.querySelectorAll('.chassis-btn').forEach(b => {
                b.className = "chassis-btn p-4 rounded-xl border border-white/10 bg-obsidian text-neutral-400 hover:text-white text-left";
            });
            btn.className = "chassis-btn active p-4 rounded-xl border border-kinetic-lime bg-kinetic-lime/10 text-white font-bold text-left";
            calcKineticSum();
        }

        function pickRimRadius(r, btn) {
            synthesizeAcousticPulse(680, 0.04);
            pickedRadius = r;
            document.querySelectorAll('.rim-btn').forEach(b => {
                b.className = "rim-btn py-3 rounded-lg border border-white/10 bg-obsidian text-center hover:border-kinetic-lime";
            });
            btn.className = "rim-btn active py-3 rounded-lg border border-kinetic-lime bg-kinetic-lime text-black font-bold text-center";
            document.getElementById('label-rim-radius').innerText = `РАДИУС R${r}`;
            calcKineticSum();
        }

        function calcKineticSum() {
            const baseCost = radiusPriceTable[pickedRadius] || 5300;
            const coeff = chassisMultiplier[pickedChassis] || 1.0;
            const finalBase = Math.round(baseCost * coeff);

            let addons = 0;
            if (document.getElementById('chk-roadforce').checked) addons += 2600;
            if (document.getElementById('chk-vault').checked) addons += 4500;
            if (document.getElementById('chk-nitro').checked) addons += 1000;
            if (document.getElementById('chk-wash').checked) addons += 1200;

            const total = finalBase + addons;

            document.getElementById('sub-base').innerText = `${finalBase.toLocaleString('ru-RU')} ₽`;
            document.getElementById('sub-addons').innerText = `${addons.toLocaleString('ru-RU')} ₽`;

            animateRollNumber(total);
        }

        function animateRollNumber(target) {
            const el = document.getElementById('kinetic-sum-roll');
            const startVal = animatedTotalSum;
            const dur = 350;
            const t0 = performance.now();

            function step(now) {
                const elapsed = now - t0;
                const p = Math.min(elapsed / dur, 1);
                const cur = Math.round(startVal + (target - startVal) * p);
                el.innerText = cur.toLocaleString('ru-RU');

                if (p < 1) requestAnimationFrame(step);
                else animatedTotalSum = target;
            }
            requestAnimationFrame(step);
        }

        function bookKineticBay() {
            fireToast('Бокс зарезервирован', `Сервисный пост №1 подготовлен для шасси R${pickedRadius}.`, false);
        }

        /* Initial Setup */
        window.addEventListener('DOMContentLoaded', () => {
            runV60Calc();
            calcKineticSum();
        });
    </script>
</body>
</html>

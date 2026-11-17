<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- Responsive viewport & mobile app friendliness for iPhone, iPad, Android tablets & phones -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <title>Little Explorers Playland</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        * {
            box-sizing: border-box;
            user-select: none;
            -webkit-user-select: none;
            -webkit-touch-callout: none;
            -webkit-tap-highlight-color: transparent;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            min-height: 100dvh;
            overflow-x: hidden;
            /* Offline-safe rounded font stack suitable for toddlers */
            font-family: 'SF Pro Rounded', 'Nunito', 'Quicksand', 'Comic Sans MS', ui-rounded, system-ui, -apple-system, sans-serif;
            background: linear-gradient(180deg, #60a5fa 0%, #93c5fd 42%, #bae6fd 72%, #86efac 72%, #4ade80 100%);
        }

        /* --- FLOATING SKY & MEADOW DECORATIONS --- */
        @keyframes floatSlow {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(3deg); }
        }

        @keyframes pulseGlow {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.07); }
        }

        @keyframes driftCloud {
            0% { transform: translateX(-160px); }
            100% { transform: translateX(calc(100vw + 180px)); }
        }

        .sun-orb {
            animation: pulseGlow 4.5s ease-in-out infinite;
        }

        .mascot-float {
            animation: floatSlow 3.2s ease-in-out infinite;
        }

        .cloud-drift-1 {
            animation: driftCloud 42s linear infinite;
        }

        .cloud-drift-2 {
            animation: driftCloud 58s linear infinite;
            animation-delay: -20s;
        }

        /* Tactile 3D Bouncy Card Styling */
        .game-card {
            transition: transform 0.22s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.22s ease;
        }
        .game-card:hover {
            transform: translateY(-6px) scale(1.02);
        }
        .game-card:active {
            transform: translateY(4px) scale(0.98);
        }

        /* Tactile 3D Play Button */
        .play-pill-btn {
            transition: transform 0.12s ease, box-shadow 0.12s ease;
        }
        .play-pill-btn:active {
            transform: translateY(5px);
        }

        /* Custom scrollbar hiding for clean embedded modal view */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="relative flex flex-col justify-between items-center text-slate-800">

    <!-- CHEERFUL ANIMATED BACKGROUND SCENE (100% OFFLINE SVG & CSS) -->
    <div class="fixed inset-0 pointer-events-none overflow-hidden z-0" aria-hidden="true">
        <!-- Smiling Sun -->
        <div class="sun-orb absolute -top-6 -right-6 sm:top-4 sm:right-8 w-28 h-28 sm:w-36 sm:h-36 rounded-full bg-gradient-to-br from-yellow-200 via-yellow-300 to-amber-400 shadow-[0_0_50px_rgba(253,224,71,0.85)] flex items-center justify-center">
            <svg viewBox="0 0 100 100" class="w-20 h-20">
                <circle cx="38" cy="44" r="5" fill="#78350f"/>
                <circle cx="62" cy="44" r="5" fill="#78350f"/>
                <circle cx="40" cy="42" r="2" fill="#ffffff"/>
                <circle cx="64" cy="42" r="2" fill="#ffffff"/>
                <path d="M38 58 Q50 70 62 58" stroke="#78350f" stroke-width="4.5" fill="none" stroke-linecap="round"/>
                <ellipse cx="29" cy="53" rx="5" ry="3" fill="#fb7185" opacity="0.6"/>
                <ellipse cx="71" cy="53" rx="5" ry="3" fill="#fb7185" opacity="0.6"/>
            </svg>
        </div>

        <!-- Fluffy Clouds -->
        <div class="cloud-drift-1 absolute top-12 left-0 opacity-90">
            <svg width="140" height="55" viewBox="0 0 140 55" fill="white">
                <path d="M30 50 H115 A20 20 0 0 0 115 12 A28 28 0 0 0 62 8 A22 22 0 0 0 30 50 Z"/>
            </svg>
        </div>
        <div class="cloud-drift-2 absolute top-28 left-0 opacity-80">
            <svg width="110" height="45" viewBox="0 0 140 55" fill="white">
                <path d="M30 50 H115 A20 20 0 0 0 115 12 A28 28 0 0 0 62 8 A22 22 0 0 0 30 50 Z"/>
            </svg>
        </div>

        <!-- Rolling Hills & Flowers at Bottom -->
        <svg class="absolute bottom-0 left-0 w-full h-36 sm:h-48" viewBox="0 0 1440 220" preserveAspectRatio="none">
            <path fill="#86efac" d="M0,90 C360,20 720,150 1080,70 C1260,30 1380,65 1440,80 L1440,220 L0,220 Z"/>
            <path fill="#4ade80" d="M0,130 C420,180 860,60 1440,120 L1440,220 L0,220 Z"/>
        </svg>
    </div>

    <!-- MAIN CONTENT WRAPPER -->
    <div class="relative z-10 w-full max-w-5xl px-4 sm:px-6 pt-5 pb-10 flex flex-col items-center flex-1">

        <!-- TOP HEADER & SOUND TOGGLE -->
        <header class="w-full flex items-center justify-between gap-3 mb-4 sm:mb-6">
            <div class="flex items-center gap-2.5 bg-white/95 border-4 border-yellow-300 rounded-full px-4 py-2 shadow-[0_5px_0_#eab308]">
                <span class="text-2xl">🎈</span>
                <span class="font-extrabold text-sky-700 text-base sm:text-lg tracking-wide">Toddler Playland</span>
            </div>

            <button id="btn-sound-toggle" aria-label="Toggle Cheerful Sounds"
                class="bg-white/95 border-4 border-pink-300 rounded-full px-4 py-2 shadow-[0_5px_0_#ec4899] active:translate-y-1 flex items-center gap-2 font-extrabold text-pink-600 text-sm sm:text-base cursor-pointer">
                <span id="sound-icon" class="text-xl">🔊</span>
                <span id="sound-label" class="hidden sm:inline">Sound On</span>
            </button>
        </header>

        <!-- HERO WELCOME BANNER -->
        <section class="text-center max-w-2xl mx-auto mb-7 sm:mb-10">
            <div class="inline-flex items-center gap-2 bg-amber-300 text-amber-950 font-extrabold text-xs sm:text-sm uppercase tracking-wider px-4 py-1.5 rounded-full border-2 border-white shadow-sm mb-3">
                <span>✨ Safe • Colorful • Offline Ready ✨</span>
            </div>

            <h1 class="text-4xl sm:text-6xl font-black text-white tracking-tight leading-tight drop-shadow-[0_5px_0_rgba(3,105,161,0.85)]">
                Pick a Fun Game!
            </h1>

            <p class="mt-2 sm:mt-3 text-base sm:text-xl font-bold text-sky-950/85 bg-white/75 backdrop-blur-sm rounded-2xl px-5 py-2 inline-block border-2 border-white/80">
                Tap any big picture below to start playing and learning!
            </p>
        </section>

        <!-- DYNAMIC GAMES GRID (POPULATED FROM SIMPLE `GAMES` LIST IN SCRIPT) -->
        <main id="games-grid" class="w-full grid grid-cols-1 md:grid-cols-2 gap-6 sm:gap-8 max-w-4xl mx-auto">
            <!-- Game cards are rendered automatically from the GAMES configuration array -->
        </main>

        <!-- PARENT / DEVELOPER QUICK ADD NOTE FOOTER -->
        <footer class="mt-10 sm:mt-14 text-center">
            <div class="inline-flex flex-wrap items-center justify-center gap-2 bg-white/85 backdrop-blur-sm border-2 border-white rounded-full px-5 py-2 shadow-md text-xs sm:text-sm font-bold text-emerald-900">
                <span>🌟 Designed for Little Fingers & Big Smiles</span>
                <span class="hidden sm:inline">•</span>
                <span>Works on iPhone, iPad & Android</span>
            </div>
        </footer>
    </div>

    <!-- LAUNCH / IN-APP GAME MODAL (OPENS LINKED GAME FILE OR BUILT-IN PREVIEW) -->
    <div id="game-launch-modal" class="fixed inset-0 z-50 bg-sky-950/75 backdrop-blur-md hidden flex items-center justify-center p-3 sm:p-5">
        <div class="relative w-full max-w-3xl h-[88dvh] bg-white border-6 border-yellow-300 rounded-[34px] shadow-2xl overflow-hidden flex flex-col">
            <!-- Modal Top Bar with Big Toddler-Friendly Back Home Button -->
            <div class="bg-gradient-to-r from-sky-400 to-blue-500 px-4 py-3 flex items-center justify-between border-b-4 border-white shrink-0">
                <button id="btn-close-modal"
                    class="bg-yellow-300 hover:bg-yellow-200 text-amber-950 font-black text-base sm:text-lg px-5 py-2 rounded-full border-4 border-white shadow-[0_4px_0_#ca8a04] active:translate-y-1 flex items-center gap-2 cursor-pointer">
                    <svg class="w-6 h-6" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M12 3L2 12h3v8h6v-6h2v6h6v-8h3L12 3z"/>
                    </svg>
                    <span>All Games</span>
                </button>

                <span id="modal-game-title" class="text-white font-black text-lg sm:text-2xl drop-shadow">
                    Game Title
                </span>

                <a id="modal-open-tab" href="#" target="_blank" rel="noopener"
                   class="bg-white/25 hover:bg-white/35 text-white font-bold text-xs sm:text-sm px-3.5 py-2 rounded-full border-2 border-white/70">
                    Full Screen ↗
                </a>
            </div>

            <!-- Game Frame Container -->
            <div class="relative flex-1 w-full bg-sky-100 overflow-hidden">
                <iframe id="game-iframe" title="Active Toddler Game" class="w-full h-full border-0"></iframe>
            </div>
        </div>
    </div>

    <script>
        /**
         * ============================================================================
         *  EASY-TO-EXTEND GAMES REGISTRY
         *  To add a new game in the future, simply copy one object block below and
         *  paste it into the `GAMES` array with your new title, file path, and icon!
         * ============================================================================
         */
        const GAMES = [
            {
                id: 'tetris-shark',
                title: 'Tetris Shark',
                badge: 'Ocean Fun',
                ageTag: 'Ages 2–6',
                description: 'Stack cute baby sharks under the sea! Pop bubbles and make a splash!',
                fileUrl: 'index.html', // Link to your Tetris Shark HTML file
                cardGradient: 'from-cyan-400 via-sky-400 to-blue-500',
                borderColor: 'border-yellow-300',
                shadowColor: 'shadow-[0_10px_0_#0284c7,0_18px_30px_rgba(0,0,0,0.22)]',
                btnGradient: 'from-amber-300 to-orange-400',
                btnShadow: 'shadow-[0_6px_0_#c2410c]',
                btnTextColor: 'text-amber-950',
                // Custom Inline SVG Mascot Illustration (100% Offline, No Broken Images)
                illustrationSvg: `
                    <svg viewBox="0 0 240 160" class="w-48 h-32 sm:w-56 sm:h-36 mascot-float drop-shadow-md">
                        <!-- Floating Bubbles -->
                        <circle cx="38" cy="36" r="8" fill="rgba(255,255,255,0.65)" stroke="white" stroke-width="2"/>
                        <circle cx="204" cy="30" r="10" fill="rgba(255,255,255,0.65)" stroke="white" stroke-width="2"/>
                        <circle cx="192" cy="54" r="5" fill="rgba(255,255,255,0.65)"/>

                        <!-- Cute Pink Mini Shark Block Top-Left -->
                        <g transform="translate(26, 56) rotate(-10)">
                            <path d="M18,0 Q24,-12 32,0 Z" fill="#d63375"/>
                            <rect x="0" y="0" width="46" height="42" rx="12" fill="#ff66a3" stroke="#ffffff" stroke-width="3"/>
                            <rect x="4" y="27" width="38" height="11" rx="6" fill="#fff0f6"/>
                            <circle cx="15" cy="17" r="4.5" fill="white"/>
                            <circle cx="16" cy="17" r="2.5" fill="#111"/>
                            <circle cx="31" cy="17" r="4.5" fill="white"/>
                            <circle cx="30" cy="17" r="2.5" fill="#111"/>
                            <path d="M19,23 Q23,27 27,23" stroke="#111" stroke-width="2" fill="none" stroke-linecap="round"/>
                        </g>

                        <!-- Cute Green Mini Shark Block Top-Right -->
                        <g transform="translate(166, 52) rotate(10)">
                            <path d="M16,0 Q23,-12 30,0 Z" fill="#1fa830"/>
                            <rect x="0" y="0" width="46" height="42" rx="12" fill="#38e54d" stroke="#ffffff" stroke-width="3"/>
                            <rect x="4" y="27" width="38" height="11" rx="6" fill="#ebffee"/>
                            <circle cx="15" cy="17" r="4.5" fill="white"/>
                            <circle cx="16" cy="17" r="2.5" fill="#111"/>
                            <circle cx="31" cy="17" r="4.5" fill="white"/>
                            <circle cx="30" cy="17" r="2.5" fill="#111"/>
                            <path d="M19,23 Q23,27 27,23" stroke="#111" stroke-width="2" fill="none" stroke-linecap="round"/>
                        </g>

                        <!-- Main Hero Yellow Baby Shark Center -->
                        <g transform="translate(45, 22)">
                            <!-- Dorsal Fin -->
                            <path d="M68,26 Q78,-4 98,26 Z" fill="#ffde00" stroke="#ffffff" stroke-width="3.5" stroke-linejoin="round"/>
                            <!-- Tail Fin -->
                            <path d="M26,64 L4,40 Q13,64 4,88 L26,64 Z" fill="#ffde00" stroke="#ffffff" stroke-width="3.5" stroke-linejoin="round"/>
                            <!-- Shark Body -->
                            <ellipse cx="82" cy="64" rx="58" ry="36" fill="#ffde00" stroke="#ffffff" stroke-width="4"/>
                            <!-- White Belly -->
                            <path d="M32,70 Q82,106 136,70 Q88,84 32,70 Z" fill="#ffffff"/>
                            <!-- Side Fin -->
                            <path d="M74,74 Q58,102 88,88 Z" fill="#ffde00" stroke="#f59e0b" stroke-width="3" stroke-linejoin="round"/>
                            <!-- Big Sparkly Eye -->
                            <circle cx="114" cy="54" r="11" fill="#ffffff" stroke="#1e293b" stroke-width="2.5"/>
                            <circle cx="117" cy="53" r="6" fill="#0f172a"/>
                            <circle cx="119" cy="50" r="2.5" fill="#ffffff"/>
                            <!-- Rosy Cheek -->
                            <ellipse cx="102" cy="67" rx="6" ry="3.5" fill="#ff66a3" opacity="0.8"/>
                            <!-- Big Smile -->
                            <path d="M116,72 Q127,79 136,70" stroke="#0f172a" stroke-width="3" fill="none" stroke-linecap="round"/>
                        </g>
                    </svg>
                `
            },
            {
                id: 'abc-tracing',
                title: 'ABC Letter Tracing',
                badge: 'Learn ABCs',
                ageTag: 'Ages 2–5',
                description: 'Trace big capital letters with your finger and earn shiny gold stars!',
                fileUrl: 'abc_tracing.html', // Link to your ABC Letter Tracing HTML file
                cardGradient: 'from-pink-400 via-rose-400 to-orange-400',
                borderColor: 'border-yellow-300',
                shadowColor: 'shadow-[0_10px_0_#be185d,0_18px_30px_rgba(0,0,0,0.22)]',
                btnGradient: 'from-emerald-300 to-green-500',
                btnShadow: 'shadow-[0_6px_0_#15803d]',
                btnTextColor: 'text-white',
                // Custom Inline SVG Mascot Illustration (100% Offline, No Broken Images)
                illustrationSvg: `
                    <svg viewBox="0 0 240 160" class="w-48 h-32 sm:w-56 sm:h-36 mascot-float drop-shadow-md">
                        <!-- Mini Floating Stars -->
                        <polygon points="34,26 38,35 48,36 40,43 42,52 34,47 26,52 28,43 20,36 30,35" fill="#ffde00" stroke="white" stroke-width="2"/>
                        <polygon points="204,24 207,31 215,32 209,37 211,45 204,41 197,45 199,37 193,32 201,31" fill="#ffde00" stroke="white" stroke-width="2"/>

                        <!-- Cute Tracing Card Board -->
                        <rect x="46" y="16" width="148" height="126" rx="28" fill="#ffffff" stroke="#ffde00" stroke-width="6"/>

                        <!-- Big Rounded Capital Letter A Track -->
                        <path d="M120 38 L86 118 M120 38 L154 118 M97 92 L143 92"
                              stroke="#e2e8f0" stroke-width="20" stroke-linecap="round" stroke-linejoin="round" fill="none"/>

                        <!-- Colorful Traced Stroke Overlay -->
                        <path d="M120 38 L86 118 M120 38 L142 90"
                              stroke="#ff595e" stroke-width="15" stroke-linecap="round" stroke-linejoin="round" fill="none"/>

                        <!-- Dashed Guide Line -->
                        <path d="M142 90 L154 118 M97 92 L143 92"
                              stroke="#94a3b8" stroke-width="3.5" stroke-dasharray="6 6" stroke-linecap="round" fill="none"/>

                        <!-- Glowing Target Dot & Cute Pointer -->
                        <circle cx="142" cy="90" r="11" fill="#ffde00" stroke="#ff8c00" stroke-width="3"/>
                        <text x="148" y="122" font-size="34">👆</text>

                        <!-- Smiling Gold Star Badge on Corner -->
                        <g transform="translate(184, 114) rotate(12)">
                            <polygon points="0,-24 7,-8 24,-6 11,6 15,23 0,14 -15,23 -11,6 -24,-6 -7,-8"
                                     fill="#ffde00" stroke="#ff8c00" stroke-width="3" stroke-linejoin="round"/>
                            <circle cx="-5" cy="-2" r="2.2" fill="#222"/>
                            <circle cx="5" cy="-2" r="2.2" fill="#222"/>
                            <path d="M-4,4 Q0,8 4,4" stroke="#222" stroke-width="2" fill="none" stroke-linecap="round"/>
                        </g>
                    </svg>
                `
            }
        ];

        // --- 2. CHEERFUL OFFLINE WEB AUDIO & VOICE FEEDBACK ---
        let soundEnabled = true;
        let audioCtx = null;

        function initAudio() {
            if (!soundEnabled) return;
            try {
                if (!audioCtx) {
                    const AudioContextClass = window.AudioContext || window.webkitAudioContext;
                    if (AudioContextClass) audioCtx = new AudioContextClass();
                }
                if (audioCtx && audioCtx.state === 'suspended') {
                    audioCtx.resume();
                }
            } catch (e) {}
        }

        function playHappyPop() {
            if (!soundEnabled) return;
            initAudio();
            if (!audioCtx) return;

            const now = audioCtx.currentTime;
            const notes = [523.25, 659.25, 783.99, 1046.50]; // C5 - E5 - G5 - C6
            notes.forEach((freq, idx) => {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(freq, now + idx * 0.06);

                gain.gain.setValueAtTime(0.001, now + idx * 0.06);
                gain.gain.linearRampToValueAtTime(0.22, now + idx * 0.06 + 0.015);
                gain.gain.exponentialRampToValueAtTime(0.001, now + idx * 0.06 + 0.18);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now + idx * 0.06);
                osc.stop(now + idx * 0.06 + 0.2);
            });
        }

        function speakCheerfully(text) {
            if (!soundEnabled || !('speechSynthesis' in window)) return;
            try {
                window.speechSynthesis.cancel();
                const utter = new SpeechSynthesisUtterance(text);
                const voices = window.speechSynthesis.getVoices();
                const friendly = voices.find(v =>
                    /samantha|karen|aria|jenny|zira|google us english/i.test(v.name)
                );
                if (friendly) utter.voice = friendly;
                utter.rate = 1.05;
                utter.pitch = 1.45;
                window.speechSynthesis.speak(utter);
            } catch (e) {}
        }

        // Toggle Sound Button
        const soundBtn = document.getElementById('btn-sound-toggle');
        const soundIcon = document.getElementById('sound-icon');
        const soundLabel = document.getElementById('sound-label');

        soundBtn.addEventListener('click', () => {
            soundEnabled = !soundEnabled;
            soundIcon.textContent = soundEnabled ? '🔊' : '🔇';
            soundLabel.textContent = soundEnabled ? 'Sound On' : 'Muted';
            if (soundEnabled) {
                playHappyPop();
                speakCheerfully("Yay! Let's play!");
            } else if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
            }
        });

        // --- 3. RENDER GAME CARDS FROM `GAMES` ARRAY ---
        const gamesGrid = document.getElementById('games-grid');
        const modal = document.getElementById('game-launch-modal');
        const gameIframe = document.getElementById('game-iframe');
        const modalTitle = document.getElementById('modal-game-title');
        const modalOpenTab = document.getElementById('modal-open-tab');

        function renderGameCards() {
            gamesGrid.innerHTML = '';

            GAMES.forEach(game => {
                const card = document.createElement('article');
                card.className = `game-card cursor-pointer rounded-[36px] border-6 ${game.borderColor} bg-gradient-to-b ${game.cardGradient} ${game.shadowColor} p-5 sm:p-7 flex flex-col items-center text-center relative overflow-hidden`;
                card.setAttribute('role', 'button');
                card.setAttribute('tabindex', '0');
                card.setAttribute('aria-label', `Play ${game.title}`);

                card.innerHTML = `
                    <!-- Top Decorative Shine -->
                    <div class="absolute -top-12 -left-12 w-40 h-40 bg-white/20 rounded-full pointer-events-none"></div>

                    <!-- Top Pills: Theme Badge & Age Tag -->
                    <div class="w-full flex items-center justify-between gap-2 mb-2 z-10">
                        <span class="bg-white/90 text-slate-800 font-extrabold text-xs sm:text-sm px-3.5 py-1 rounded-full shadow-sm">
                            ${game.badge}
                        </span>
                        <span class="bg-black/20 text-white font-extrabold text-xs sm:text-sm px-3.5 py-1 rounded-full">
                            ${game.ageTag}
                        </span>
                    </div>

                    <!-- Center Mascot Illustration -->
                    <div class="my-2 sm:my-3 flex items-center justify-center z-10">
                        ${game.illustrationSvg}
                    </div>

                    <!-- Game Title -->
                    <h2 class="text-2xl sm:text-3xl font-black text-white drop-shadow-[0_3px_0_rgba(0,0,0,0.25)] tracking-wide z-10">
                        ${game.title}
                    </h2>

                    <!-- Toddler-Friendly Short Description -->
                    <p class="mt-2 text-white/95 font-bold text-sm sm:text-base leading-snug max-w-xs z-10">
                        ${game.description}
                    </p>

                    <!-- Big Tactile PLAY Button -->
                    <div class="mt-5 w-full max-w-[230px] z-10">
                        <div class="play-pill-btn w-full py-3.5 px-6 rounded-full border-4 border-white bg-gradient-to-b ${game.btnGradient} ${game.btnShadow} ${game.btnTextColor} font-black text-xl sm:text-2xl flex items-center justify-center gap-2.5">
                            <svg class="w-7 h-7" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M8 5v14l11-7z"/>
                            </svg>
                            <span>PLAY!</span>
                        </div>
                    </div>
                `;

                const launchHandler = () => openGame(game);
                card.addEventListener('click', launchHandler);
                card.addEventListener('keydown', (e) => {
                    if (e.key === 'Enter' || e.key === ' ') {
                        e.preventDefault();
                        launchHandler();
                    }
                });

                gamesGrid.appendChild(card);
            });
        }

        // --- 4. LAUNCH GAME IN MODAL OR NEW TAB ---
        function openGame(game) {
            playHappyPop();
            speakCheerfully(`Let's play ${game.title}!`);

            modalTitle.textContent = game.title;
            modalOpenTab.href = game.fileUrl;
            gameIframe.src = game.fileUrl;
            modal.classList.remove('hidden');
        }

        function closeGameModal() {
            playHappyPop();
            modal.classList.add('hidden');
            gameIframe.src = 'about:blank';
        }

        document.getElementById('btn-close-modal').addEventListener('click', closeGameModal);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) closeGameModal();
        });

        // Preload voices on mobile/desktop
        if ('speechSynthesis' in window) {
            window.speechSynthesis.getVoices();
            window.speechSynthesis.onvoiceschanged = () => window.speechSynthesis.getVoices();
        }

        // Initial Render
        renderGameCards();
    </script>
</body>
</html>

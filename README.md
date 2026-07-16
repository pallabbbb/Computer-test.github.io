<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CompHistory • Abacus to AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&amp;family=Space+Grotesk:wght@500;600&amp;display=swap');
        body { font-family: 'Inter', system_ui, sans-serif; }
        .font-display { font-family: 'Space Grotesk', 'Inter', sans-serif; font-weight: 600; }

        /* Cool Intro Animation */
        #intro-screen { background: radial-gradient(circle at center, #0f172a 0%, #020617 100%); }
        .circuit-line {
            position: absolute; background: linear-gradient(90deg, transparent, #6366f1, transparent);
            height: 1px; animation: circuitMove 3s linear infinite; opacity: 0.3;
        }
        @keyframes circuitMove { 0% { transform: translateX(-100%); } 100% { transform: translateX(400%); } }
        .intro-logo { animation: logoPop 1.2s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
        .intro-text { animation: fadeUp 1s ease forwards; animation-delay: 1.2s; opacity: 0; }
        .stagger-1 { animation-delay: 1.4s; } .stagger-2 { animation-delay: 1.6s; }
        @keyframes logoPop { 0% { transform: scale(0.6); opacity: 0; } 60% { transform: scale(1.1); } 100% { transform: scale(1); opacity: 1; } }
        @keyframes fadeUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .particle { position: absolute; width: 4px; height: 4px; background: #6366f1; border-radius: 50%; animation: float 4s ease-in-out infinite; opacity: 0.6; }

        .quiz-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .quiz-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 25px 50px -12px rgb(0 0 0 / 0.15);
        }

        .option-label {
            transition: all 0.2s;
        }
        .option-label:hover {
            background-color: #f1f5f9;
        }
    </style>
</head>
<body class="bg-slate-50">

    <!-- COOL INTRO ANIMATION -->
    <div id="intro-screen" class="fixed inset-0 z-[999] flex items-center justify-center overflow-hidden">
        <div class="absolute inset-0">
            <div class="circuit-line top-[20%]" style="width: 60%; left: 10%; animation-delay: 0s;"></div>
            <div class="circuit-line top-[35%]" style="width: 40%; left: 30%; animation-delay: 1.2s;"></div>
            <div class="circuit-line top-[65%]" style="width: 70%; left: 15%; animation-delay: 2.5s;"></div>
            <div class="circuit-line top-[80%]" style="width: 50%; left: 40%; animation-delay: 0.8s;"></div>
        </div>
        <div id="particles-container" class="absolute inset-0 pointer-events-none"></div>

        <div class="relative z-10 text-center px-6">
            <div class="flex justify-center mb-6">
                <div class="w-20 h-20 bg-indigo-600 rounded-3xl flex items-center justify-center shadow-2xl intro-logo">
                    <i class="fa-solid fa-microchip text-white text-5xl"></i>
                </div>
            </div>
            <h1 class="font-display text-7xl tracking-tighter font-bold text-white mb-3 intro-text">CompHistory</h1>
            <div class="flex justify-center gap-x-3 text-xl text-indigo-300 font-medium mb-8">
                <span class="intro-text stagger-1">Learn</span>
                <span class="intro-text stagger-2">•</span>
                <span class="intro-text stagger-1">Test</span>
                <span class="intro-text stagger-2">•</span>
                <span class="intro-text stagger-1">Master</span>
            </div>
            <p class="text-slate-400 text-sm tracking-widest">COMPUTER HISTORY • FROM ABACUS TO AI</p>
        </div>
        <div class="absolute bottom-8 text-center">
            <p class="text-xs text-slate-500 tracking-widest">CLICK ANYWHERE TO CONTINUE</p>
        </div>
    </div>

    <!-- Auth Screen -->
    <div id="auth-screen" class="min-h-screen flex items-center justify-center bg-gradient-to-br from-slate-900 to-indigo-950 p-6 hidden">
        <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl p-8">
            <div class="text-center mb-8">
                <div class="w-16 h-16 bg-indigo-600 rounded-2xl flex items-center justify-center mx-auto mb-4">
                    <i class="fa-solid fa-microchip text-white text-4xl"></i>
                </div>
                <h1 class="font-display text-4xl font-bold tracking-tighter">CompHistory</h1>
                <p class="text-slate-500 mt-1">Learn • Test • Master</p>
            </div>

            <div id="auth-tabs" class="flex mb-6 bg-slate-100 rounded-2xl p-1">
                <button id="login-tab" class="flex-1 py-2.5 rounded-xl font-semibold text-sm transition-all bg-white shadow">Login</button>
                <button id="signup-tab" class="flex-1 py-2.5 rounded-xl font-semibold text-sm transition-all text-slate-500">Sign Up</button>
            </div>

            <div id="login-form">
                <div class="space-y-4">
                    <div>
                        <label class="text-xs font-semibold tracking-wider text-slate-500 block mb-1.5">USERNAME</label>
                        <input id="login-username" type="text" maxlength="16" class="w-full border border-slate-300 px-4 py-3 rounded-2xl text-sm focus:outline-none focus:border-indigo-500" placeholder="Username (max 16)">
                    </div>
                    <div>
                        <label class="text-xs font-semibold tracking-wider text-slate-500 block mb-1.5">PASSWORD</label>
                        <input id="login-password" type="password" maxlength="12" class="w-full border border-slate-300 px-4 py-3 rounded-2xl text-sm focus:outline-none focus:border-indigo-500" placeholder="Password (max 12)">
                    </div>
                    <button onclick="loginUser()" class="w-full py-3.5 bg-indigo-600 hover:bg-indigo-700 transition-colors text-white font-semibold rounded-3xl">Login</button>
                </div>
            </div>

            <div id="signup-form" class="hidden">
                <div class="space-y-4">
                    <div>
                        <label class="text-xs font-semibold tracking-wider text-slate-500 block mb-1.5">USERNAME</label>
                        <input id="signup-username" type="text" maxlength="16" class="w-full border border-slate-300 px-4 py-3 rounded-2xl text-sm focus:outline-none focus:border-indigo-500" placeholder="Username (max 16)">
                    </div>
                    <div>
                        <label class="text-xs font-semibold tracking-wider text-slate-500 block mb-1.5">PASSWORD</label>
                        <input id="signup-password" type="password" maxlength="12" class="w-full border border-slate-300 px-4 py-3 rounded-2xl text-sm focus:outline-none focus:border-indigo-500" placeholder="Password (max 12)">
                    </div>
                    <button onclick="signupUser()" class="w-full py-3.5 bg-emerald-600 hover:bg-emerald-700 transition-colors text-white font-semibold rounded-3xl">Create Account</button>
                </div>
            </div>

            <p class="text-center text-xs text-slate-400 mt-6">Demo Mode — Any username/password works</p>
        </div>
    </div>

    <!-- Main App -->
    <div id="main-app" class="hidden">
        <nav class="bg-white border-b border-slate-200 sticky top-0 z-50">
            <div class="max-w-7xl mx-auto px-6 py-4">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-x-3">
                        <div class="w-11 h-11 bg-indigo-600 rounded-2xl flex items-center justify-center">
                            <i class="fa-solid fa-microchip text-white text-3xl"></i>
                        </div>
                        <span class="font-display text-3xl font-semibold tracking-tighter">CompHistory</span>
                    </div>
                    <div class="flex items-center gap-x-6">
                        <button onclick="showStudyModal()" class="px-4 py-2 flex items-center gap-x-2 hover:bg-slate-100 rounded-3xl text-sm font-medium">
                            <i class="fa-solid fa-book text-indigo-500"></i> 
                            <span>Study Notes</span>
                        </button>
                        <div class="flex items-center gap-x-2">
                            <div class="w-8 h-8 bg-slate-200 rounded-2xl flex items-center justify-center text-slate-600">
                                👤
                            </div>
                            <span id="username-display" class="font-medium text-sm"></span>
                        </div>
                    </div>
                </div>
            </div>
        </nav>

        <!-- Home -->
        <div id="home-section" class="max-w-7xl mx-auto px-6 pt-10 pb-16">
            <div class="text-center mb-12">
                <h1 class="font-display text-6xl tracking-tighter font-semibold text-slate-900 mb-3">Learn • Test • Improve</h1>
                <p class="text-xl text-slate-600 max-w-md mx-auto">Master the fascinating journey of computing from the Abacus to Artificial Intelligence.</p>
                <div class="flex justify-center mt-8">
                    <button onclick="showStudyModal()" class="px-10 py-4 bg-gradient-to-r from-indigo-600 to-violet-600 text-white font-semibold rounded-3xl flex items-center gap-x-3 hover:shadow-xl transition-all">
                        <i class="fa-solid fa-book"></i>
                        Start Learning
                    </button>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-5xl mx-auto">
                <!-- Easy -->
                <div onclick="startQuiz('easy')" class="quiz-card bg-white border border-slate-200 hover:border-emerald-300 rounded-3xl p-7 cursor-pointer">
                    <div class="flex justify-between items-start mb-6">
                        <div>
                            <div class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-2xl flex items-center justify-center mb-4">
                                <i class="fa-solid fa-check-double text-3xl"></i>
                            </div>
                            <h3 class="font-display text-3xl font-semibold">Easy</h3>
                            <p class="text-emerald-600">Multiple Choice • 10 Questions</p>
                        </div>
                    </div>
                    <div class="mt-8 pt-6 border-t text-emerald-600 font-semibold flex items-center gap-x-2">Start Easy Test <i class="fa-solid fa-arrow-right"></i></div>
                </div>

                <!-- Medium -->
                <div onclick="startQuiz('medium')" class="quiz-card bg-white border border-slate-200 hover:border-amber-300 rounded-3xl p-7 cursor-pointer">
                    <div class="flex justify-between items-start mb-6">
                        <div>
                            <div class="w-12 h-12 bg-amber-100 text-amber-600 rounded-2xl flex items-center justify-center mb-4">
                                <i class="fa-solid fa-keyboard text-3xl"></i>
                            </div>
                            <h3 class="font-display text-3xl font-semibold">Medium</h3>
                            <p class="text-amber-600">Short Answer • 8 Questions</p>
                        </div>
                    </div>
                    <div class="mt-8 pt-6 border-t text-amber-600 font-semibold flex items-center gap-x-2">Start Medium Test <i class="fa-solid fa-arrow-right"></i></div>
                </div>

                <!-- Hard -->
                <div onclick="startQuiz('hard')" class="quiz-card bg-white border border-slate-200 hover:border-rose-300 rounded-3xl p-7 cursor-pointer">
                    <div class="flex justify-between items-start mb-6">
                        <div>
                            <div class="w-12 h-12 bg-rose-100 text-rose-600 rounded-2xl flex items-center justify-center mb-4">
                                <i class="fa-solid fa-pen-nib text-3xl"></i>
                            </div>
                            <h3 class="font-display text-3xl font-semibold">Hard</h3>
                            <p class="text-rose-600">Essay Style • 4 Questions</p>
                        </div>
                    </div>
                    <div class="mt-8 pt-6 border-t text-rose-600 font-semibold flex items-center gap-x-2">Start Hard Test <i class="fa-solid fa-arrow-right"></i></div>
                </div>
            </div>
        </div>

        <!-- Quiz Section -->
        <div id="quiz-section" class="max-w-4xl mx-auto px-6 pb-20 hidden">
            <div class="bg-white rounded-3xl border border-slate-100 overflow-hidden">
                <div class="px-8 pt-8 pb-6 bg-gradient-to-r from-slate-900 to-slate-800 text-white">
                    <div class="flex justify-between items-center">
                        <div>
                            <div id="quiz-level-badge" class="inline-flex px-4 py-1 rounded-3xl text-sm font-bold mb-2"></div>
                            <h2 id="quiz-title" class="font-display text-4xl font-semibold"></h2>
                        </div>
                        <button onclick="endQuiz()" class="text-white/70 hover:text-white transition-colors flex items-center gap-x-1">
                            <i class="fa-solid fa-xmark"></i> End Quiz
                        </button>
                    </div>
                    <div class="mt-4 text-sm text-slate-400">Question <span id="current-q-num">1</span> of <span id="total-qs">10</span></div>
                </div>
                <div id="questions-container" class="p-8 space-y-8"></div>
                <div class="px-8 pb-8">
                    <button onclick="submitQuiz()" id="submit-btn" class="w-full py-4 bg-indigo-600 hover:bg-indigo-700 transition-colors text-white font-semibold rounded-3xl">Submit Answers</button>
                </div>
            </div>
        </div>

        <!-- Results -->
        <div id="results-section" class="max-w-4xl mx-auto px-6 pb-20 hidden">
            <div class="bg-white rounded-3xl border border-slate-100 overflow-hidden">
                <div class="px-8 pt-8 pb-6 bg-gradient-to-r from-indigo-600 to-violet-600 text-white text-center">
                    <h2 class="font-display text-4xl font-semibold">Quiz Complete!</h2>
                    <div id="score-display" class="mt-6 text-7xl font-display font-bold"></div>
                    <p id="score-message" class="mt-2 text-indigo-100"></p>
                </div>
                <div class="p-8">
                    <div id="review-container" class="space-y-6"></div>
                    <div id="weak-areas-section" class="mt-10 hidden">
                        <h3 class="font-semibold text-xl mb-4 text-rose-600">🔄 Topics to Review</h3>
                        <div id="weak-areas-list" class="space-y-3"></div>
                    </div>
                    <div class="flex gap-4 mt-10">
                        <button onclick="retakeQuiz()" class="flex-1 py-4 bg-slate-100 hover:bg-slate-200 transition-colors rounded-3xl font-semibold">Retake This Test</button>
                        <button onclick="goHome()" class="flex-1 py-4 bg-indigo-600 hover:bg-indigo-700 transition-colors text-white rounded-3xl font-semibold">Back to Home</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Study Notes Modal -->
    <div id="study-modal" onclick="if (event.target.id === 'study-modal') hideStudyModal()" class="hidden fixed inset-0 bg-black/70 z-[100] flex items-center justify-center p-6">
        <div onclick="event.stopImmediatePropagation()" class="bg-white max-w-3xl w-full rounded-3xl p-8 max-h-[90vh] overflow-auto">
            <div class="flex justify-between items-center mb-6">
                <h3 class="font-display text-3xl font-semibold">Computer History — Study Notes</h3>
                <button onclick="hideStudyModal()" class="text-slate-400 hover:text-slate-600">
                    <i class="fa-solid fa-xmark text-2xl"></i>
                </button>
            </div>
            <div class="text-slate-700 space-y-6 text-[15px]">
                <div>
                    <strong class="block text-lg">1. Abacus (c. 3000 BC)</strong>
                    <p>First known calculating device. Used by Babylonians, Egyptians, and Chinese.</p>
                </div>
                <div>
                    <strong class="block text-lg">2. Pascaline (1642)</strong>
                    <p>Mechanical calculator invented by Blaise Pascal for tax calculations.</p>
                </div>
                <div>
                    <strong class="block text-lg">3. Difference Engine (1822)</strong>
                    <p>Designed by Charles Babbage — could compute mathematical tables automatically.</p>
                </div>
                <div>
                    <strong class="block text-lg">4. Analytical Engine (1837)</strong>
                    <p>Babbage's most advanced design. Contained concepts of modern computers: CPU, memory, and conditional branching.</p>
                </div>
                <div>
                    <strong class="block text-lg">5. First Generation (1940–1956)</strong>
                    <p>Vacuum tubes. ENIAC, UNIVAC. Very large, hot, and expensive.</p>
                </div>
                <div>
                    <strong class="block text-lg">6. Second Generation (1956–1963)</strong>
                    <p>Transistors. Smaller, faster, more reliable. IBM 1401.</p>
                </div>
                <div>
                    <strong class="block text-lg">7. Third Generation (1964–1971)</strong>
                    <p>Integrated Circuits (ICs). IBM System/360.</p>
                </div>
                <div>
                    <strong class="block text-lg">8. Fourth Generation (1971–Present)</strong>
                    <p>Microprocessors. Intel 4004. Personal computers (Apple II, IBM PC).</p>
                </div>
                <div>
                    <strong class="block text-lg">9. Fifth Generation (Present)</strong>
                    <p>Artificial Intelligence, Parallel Processing, Quantum Computing.</p>
                </div>
            </div>
            <button onclick="hideStudyModal()" class="mt-8 w-full py-4 bg-slate-100 hover:bg-slate-200 transition-colors rounded-3xl font-medium">Close Notes</button>
        </div>
    </div>

    <script>
        // ==================== INTRO ANIMATION ====================
        function createParticles() {
            const container = document.getElementById('particles-container');
            for (let i = 0; i < 30; i++) {
                const p = document.createElement('div');
                p.className = 'particle';
                p.style.left = Math.random() * 100 + '%';
                p.style.top = Math.random() * 100 + '%';
                p.style.animationDelay = Math.random() * 6 + 's';
                p.style.animationDuration = (3 + Math.random() * 4) + 's';
                container.appendChild(p);
            }
        }

        function hideIntro() {
            const intro = document.getElementById('intro-screen');
            intro.style.transition = 'opacity 0.8s ease';
            intro.style.opacity = '0';
            setTimeout(() => {
                intro.style.display = 'none';
                document.getElementById('auth-screen').classList.remove('hidden');
            }, 800);
        }

   

<!DOCTYPE html>
<html lang="fr" data-theme="girly-pink">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bloom Study 💖🌸🔥 - EPGE</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Chart.js pour la progression -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Poppins', sans-serif; }
        
        :root {
            --primary: #ec4899;
            --primary-hover: #db2777;
            --bg-gradient: linear-gradient(135deg, #fdf2f8 0%, #fce7f3 100%);
            --card-bg: #ffffff;
            --text-main: #1f2937;
        }

        [data-theme="lavender"] { --primary: #8b5cf6; --bg-gradient: linear-gradient(135deg, #f5f3ff 0%, #ede9fe 100%); }
        [data-theme="peach"] { --primary: #f97316; --bg-gradient: linear-gradient(135deg, #fff7ed 0%, #ffedd5 100%); }
        [data-theme="mint"] { --primary: #10b981; --bg-gradient: linear-gradient(135deg, #ecfdf5 0%, #d1fae5 100%); }
        [data-theme="skyblue"] { --primary: #0284c7; --bg-gradient: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%); }
        [data-theme="coral"] { --primary: #f43f5e; --bg-gradient: linear-gradient(135deg, #fff1f2 0%, #ffe4e6 100%); }
        [data-theme="gold"] { --primary: #d97706; --bg-gradient: linear-gradient(135deg, #fffbeb 0%, #fef3c7 100%); }

        [data-mode="dark"] { --bg-gradient: linear-gradient(135deg, #111827 0%, #1f2937 100%); --card-bg: #1f2937; --text-main: #f9fafb; }

        body { background: var(--bg-gradient); color: var(--text-main); min-height: 100vh; padding-bottom: 90px; }
        .custom-card { background-color: var(--card-bg); color: var(--text-main); }
    </style>
</head>
<body class="transition-colors duration-300">

    <!-- ÉCRAN D'AUTHENTIFICATION -->
    <div id="authModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/60 backdrop-blur-sm p-4">
        <div class="custom-card max-w-md w-full p-8 rounded-3xl shadow-2xl border border-pink-100 dark:border-gray-700 text-center space-y-6">
            <div>
                <span class="text-4xl">💖🌸🔥</span>
                <h1 class="text-2xl font-bold mt-2 bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">Bloom Study</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">Espace Prépa EPGE ECG 1 & 2</p>
            </div>

            <div class="flex border-b border-gray-200 dark:border-gray-700">
                <button id="tabLoginBtn" onclick="switchAuthTab('login')" class="flex-1 py-2 font-semibold text-pink-500 border-b-2 border-pink-500">Se connecter</button>
                <button id="tabRegisterBtn" onclick="switchAuthTab('register')" class="flex-1 py-2 font-semibold text-gray-400 border-b-2 border-transparent">Créer un compte</button>
            </div>

            <div class="space-y-4 text-left">
                <div>
                    <label class="block text-sm font-medium mb-1">Pseudo / Prénom</label>
                    <input type="text" id="authUsername" placeholder="Ex: Sarah" class="w-full p-3.5 rounded-2xl border border-gray-300 dark:border-gray-600 dark:bg-gray-700 focus:outline-none focus:border-pink-500 font-medium">
                </div>
                <div>
                    <label class="block text-sm font-medium mb-1">Mot de passe</label>
                    <input type="password" id="authPassword" placeholder="••••••••" class="w-full p-3.5 rounded-2xl border border-gray-300 dark:border-gray-600 dark:bg-gray-700 focus:outline-none focus:border-pink-500">
                </div>
                <button id="authSubmitBtn" onclick="handleAuthSubmit()" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3.5 rounded-2xl transition shadow-lg shadow-pink-500/25 mt-2">
                    Se connecter ➔
                </button>
            </div>
        </div>
    </div>

    <!-- SITE PRINCIPAL -->
    <div id="appContainer" class="hidden">
        
        <!-- HEADER -->
        <header class="bg-white/80 dark:bg-gray-800/80 backdrop-blur-md shadow-sm sticky top-0 z-40 px-4 py-3 border-b border-pink-100 dark:border-gray-700">
            <div class="max-w-7xl mx-auto flex justify-between items-center">
                <div class="flex items-center space-x-2">
                    <span class="text-xl">💖🌸🔥</span>
                    <h1 class="text-lg font-bold bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">Bloom Study</h1>
                </div>
                <div class="flex items-center space-x-3">
                    <span class="text-xs bg-pink-50 dark:bg-gray-700 px-3 py-1.5 rounded-full font-medium">👤 <strong id="headerUsername">Sarah</strong></span>
                    <button onclick="logoutUser()" class="text-xs text-red-500 font-medium">[Déconnexion]</button>
                </div>
            </div>
        </header>

        <!-- CONTENU DES ONGLETS -->
        <main class="max-w-4xl mx-auto p-4 md:p-6 mb-16">

            <!-- 1. ACCUEIL -->
            <div id="viewAccueil" class="space-y-6">
                <div class="custom-card p-6 rounded-3xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h2 class="text-2xl font-bold mb-1">Bienvenue <span class="text-pink-500" id="welcomeUsername">Sarah</span>, ravie de te voir ! ✨</h2>
                    <p class="text-gray-500 dark:text-gray-400 text-xs mb-6">Chaque effort compte, mon espace. Organise tes révisions en conditions de test.</p>
                    
                    <button onclick="openCreateTestModal()" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-4 rounded-2xl shadow-lg shadow-pink-500/25 transition mb-6">
                        Commencer un test ➔
                    </button>

                    <div class="grid grid-cols-3 gap-3 text-center">
                        <div class="p-3 rounded-2xl bg-pink-50 dark:bg-gray-700/50 border border-pink-100">
                            <span class="text-xl font-bold block" id="statCount">0</span>
                            <span class="text-[10px] text-gray-500">Tests terminés</span>
                        </div>
                        <div class="p-3 rounded-2xl bg-purple-50 dark:bg-gray-700/50 border border-purple-100">
                            <span class="text-xl font-bold block" id="statAvg">0.0</span>
                            <span class="text-[10px] text-gray-500">Moyenne générale</span>
                        </div>
                        <div class="p-3 rounded-2xl bg-amber-50 dark:bg-gray-700/50 border border-amber-100">
                            <span class="text-xl font-bold block">9/9</span>
                            <span class="text-[10px] text-gray-500">Matières ECG</span>
                        </div>
                    </div>
                </div>

                <!-- LISTE DES MATIÈRES ECG 1 & 2 -->
                <div>
                    <h3 class="font-bold text-lg mb-3">Choisis ta matière</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-3" id="subjectsGrid">
                        <!-- Généré dynamiquement -->
                    </div>
                </div>
            </div>

            <!-- 2. MES TESTS / CRÉATION -->
            <div id="viewTests" class="hidden space-y-6">
                <div class="custom-card p-6 rounded-3xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-xl font-bold">📚 Mes tests & leçons</h2>
                        <button onclick="openCreateTestModal()" class="bg-pink-500 text-white text-xs px-4 py-2 rounded-xl font-semibold">+ Créer un test</button>
                    </div>

                    <div class="space-y-4">
                        <div>
                            <label class="block text-xs font-medium mb-1">Matière</label>
                            <select id="filterSubject" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                                <option value="Tous">Toutes les matières</option>
                            </select>
                        </div>
                        <div class="bg-pink-50 dark:bg-gray-700/40 p-4 rounded-2xl border border-pink-100 space-y-3">
                            <h4 class="font-semibold text-sm text-pink-600 dark:text-pink-400">✨ Configuration d'une évaluation</h4>
                            <div>
                                <label class="block text-xs font-medium mb-1">Titre du test</label>
                                <input type="text" id="testTitleInput" placeholder="Ex: Interrogation d'analyse" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                            </div>
                            <div>
                                <label class="block text-xs font-medium mb-1">Leçon principale</label>
                                <input type="text" id="testLessonInput" placeholder="Ex: Fonctions usuelles" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                            </div>
                            <div>
                                <label class="block text-xs font-medium mb-1">Partie précise du cours à évaluer</label>
                                <input type="text" id="testPartInput" placeholder="Ex: De la dérivabilité jusqu'à l'intégration" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                            </div>
                            <div class="grid grid-cols-2 gap-2">
                                <div>
                                    <label class="block text-xs font-medium mb-1">Nombre de questions</label>
                                    <input type="number" id="testQCount" value="10" min="5" max="30" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                                </div>
                                <div>
                                    <label class="block text-xs font-medium mb-1">Durée (minutes)</label>
                                    <input type="number" id="testDuration" value="20" min="5" max="120" class="w-full p-2.5 rounded-xl border dark:bg-gray-700 text-sm">
                                </div>
                            </div>
                            <button onclick="launchCustomTest()" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 rounded-xl text-sm transition shadow-md">
                                Lancer l'évaluation personnalisée ➔
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 3. PROGRESSION -->
            <div id="viewProgression" class="hidden space-y-6">
                <div class="custom-card p-6 rounded-3xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h2 class="text-xl font-bold mb-4">📈 Suivi analytique</h2>
                    <div class="h-64"><canvas id="progressChart"></canvas></div>
                </div>
            </div>

            <!-- 4. SETTINGS (RÉGLAGES) -->
            <div id="viewSettings" class="hidden space-y-6">
                <div class="custom-card p-6 rounded-3xl shadow-lg border border-pink-100 dark:border-gray-700 space-y-6">
                    <h2 class="text-xl font-bold">⚙️ Réglages & Personnalisation</h2>
                    
                    <div>
                        <label class="block text-sm font-semibold mb-2">Palette de couleurs (Thème)</label>
                        <div class="grid grid-cols-3 gap-2">
                            <button onclick="changeColorTheme('girly-pink')" class="p-3 rounded-2xl bg-pink-100 text-pink-700 font-medium text-xs border border-pink-300">🌸 Rose Girly</button>
                            <button onclick="changeColorTheme('lavender')" class="p-3 rounded-2xl bg-purple-100 text-purple-700 font-medium text-xs border border-purple-300">💜 Lavande</button>
                            <button onclick="changeColorTheme('peach')" class="p-3 rounded-2xl bg-orange-100 text-orange-700 font-medium text-xs border border-orange-300">🍑 Pêche</button>
                            <button onclick="changeColorTheme('mint')" class="p-3 rounded-2xl bg-emerald-100 text-emerald-700 font-medium text-xs border border-emerald-300">🌿 Menthe</button>
                            <button onclick="changeColorTheme('skyblue')" class="p-3 rounded-2xl bg-sky-100 text-sky-700 font-medium text-xs border border-sky-300">☁️ Ciel</button>
                            <button onclick="changeColorTheme('coral')" class="p-3 rounded-2xl bg-rose-100 text-rose-700 font-medium text-xs border border-rose-300">🌺 Corail</button>
                            <button onclick="changeColorTheme('gold')" class="p-3 rounded-2xl bg-amber-100 text-amber-700 font-medium text-xs border border-amber-300">✨ Or</button>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-semibold mb-2">Mode d'affichage</label>
                        <button onclick="toggleDarkMode()" class="w-full py-3 rounded-2xl bg-gray-100 dark:bg-gray-700 font-medium text-sm border dark:border-gray-600">
                            🌙 Basculer Mode Sombre / Clair ☀️
                        </button>
                    </div>
                </div>
            </div>

            <!-- EXÉCUTION DU TEST -->
            <div id="viewActiveTest" class="hidden custom-card p-6 rounded-3xl shadow-lg border border-pink-100 dark:border-gray-700 space-y-6">
                <div class="flex justify-between items-center border-b pb-4 dark:border-gray-700">
                    <div>
                        <span id="activeSubjectBadge" class="text-xs bg-pink-100 text-pink-700 px-2.5 py-1 rounded-full font-semibold">Matière</span>
                        <h2 class="text-lg font-bold mt-2" id="activeTestHeading">Titre de la leçon</h2>
                    </div>
                    <div class="text-right">
                        <span class="text-xs text-gray-400 block">Temps restant</span>
                        <span id="timerDisplay" class="text-xl font-bold text-pink-500">20:00</span>
                    </div>
                </div>
                <div id="questionBox" class="space-y-4"></div>
                <button onclick="submitTestAnswers()" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3.5 rounded-2xl transition shadow-md">
                    Valider et voir mon score sur 20 ➔
                </button>
            </div>

        </main>

        <!-- NAVIGATION INFÉRIEURE -->
        <nav class="fixed bottom-0 left-0 right-0 bg-white/90 dark:bg-gray-800/90 backdrop-blur-md border-t border-pink-100 dark:border-gray-700 py-2.5 px-6 z-40">
            <div class="max-w-md mx-auto flex justify-between items-center text-xs font-semibold text-gray-500 dark:text-gray-400">
                <button onclick="switchTab('Accueil')" id="navAccueil" class="flex flex-col items-center text-pink-500">
                    <span class="text-lg">🏠</span> Accueil
                </button>
                <button onclick="switchTab('Tests')" id="navTests" class="flex flex-col items-center hover:text-pink-500">
                    <span class="text-lg">📚</span> Mes tests
                </button>
                <button onclick="switchTab('Progression')" id="navProgression" class="flex flex-col items-center hover:text-pink-500">
                    <span class="text-lg">📈</span> Progression
                </button>
                <button onclick="switchTab('Settings')" id="navSettings" class="flex flex-col items-center hover:text-pink-500">
                    <span class="text-lg">⚙️</span> Réglages
                </button>
            </div>
        </nav>
    </div>

    <script>
        const ecgSubjects = [
            { name: "Mathématiques", icon: "📐", desc: "Analyse, Algèbre, Probabilités" },
            { name: "Économie", icon: "📊", desc: "Macro, Micro, Politiques éco" },
            { name: "Géopolitique", icon: "🌍", desc: "Mondes, relations internationales" },
            { name: "Anglais", icon: "🇬🇧", desc: "Civilisation, grammaire, essais" },
            { name: "Informatique", icon: "💻", desc: "Python, algorithmique, SQL" },
            { name: "Français", icon: "📖", desc: "Culture générale & dissertation" },
            { name: "Philosophie", icon: "💬", desc: "Dissertation & analyse de concepts" },
            { name: "Espagnol", icon: "🇪🇸", desc: "Vocabulaire, expression, civilisation" },
            { name: "Allemand", icon: "🇩🇪", desc: "Grammaire, texte et expression" }
        ];

        let authMode = 'login';
        let currentUser = localStorage.getItem('bloom_current_user') || '';
        let chartInstance = null;

        window.addEventListener('DOMContentLoaded', () => {
            if(currentUser) {
                initApp();
            }
            buildSubjectsUI();
            buildSelectOptions();
        });

        function buildSubjectsUI() {
            const grid = document.getElementById('subjectsGrid');
            grid.innerHTML = ecgSubjects.map(sub => `
                <div onclick="selectSubjectForTest('${sub.name}')" class="custom-card p-4 rounded-2xl border border-pink-100 dark:border-gray-700 shadow-sm hover:shadow-md cursor-pointer transition flex items-center space-x-3">
                    <span class="text-2xl">${sub.icon}</span>
                    <div>
                        <h4 class="font-bold text-sm">${sub.name}</h4>
                        <p class="text-[10px] text-gray-400">${sub.desc}</p>
                    </div>
                </div>
            `).join('');
        }

        function buildSelectOptions() {
            const select = document.getElementById('filterSubject');
            select.innerHTML = `<option value="Tous">Toutes les matières</option>` + ecgSubjects.map(sub => `<option value="${sub.name}">${sub.name}</option>`).join('');
        }

        function switchAuthTab(mode) {
            authMode = mode;
            if(mode === 'login') {
                document.getElementById('tabLoginBtn').className = "flex-1 py-2 font-semibold text-pink-500 border-b-2 border-pink-500";
                document.getElementById('tabRegisterBtn').className = "flex-1 py-2 font-semibold text-gray-400 border-b-2 border-transparent";
                document.getElementById('authSubmitBtn').innerText = "Se connecter ➔";
            } else {
                document.getElementById('tabRegisterBtn').className = "flex-1 py-2 font-semibold text-pink-500 border-b-2 border-pink-500";
                document.getElementById('tabLoginBtn').className = "flex-1 py-2 font-semibold text-gray-400 border-b-2 border-transparent";
                document.getElementById('authSubmitBtn').innerText = "Créer mon compte ➔";
            }
        }

        function handleAuthSubmit() {
            let user = document.getElementById('authUsername').value.trim();
            let pass = document.getElementById('authPassword').value.trim();
            if(!user || !pass) { alert("Remplis tous les champs !"); return; }

            let users = JSON.parse(localStorage.getItem('bloom_users') || '{}');
            if(authMode === 'register') {
                if(users[user]) { alert("Ce compte existe déjà. Clique sur 'Se connecter'."); return; }
                users[user] = { pass: pass, scores: [] };
            } else {
                if(!users[user] || use

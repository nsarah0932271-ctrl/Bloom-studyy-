<!DOCTYPE html>
<html lang="fr" data-theme="girly-pink">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>N_Sarah Prep Hub - EPGE</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Chart.js pour les courbes de progression -->
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
            --text-sub: #4b5563;
        }

        [data-theme="lavender"] {
            --primary: #8b5cf6;
            --primary-hover: #7c3aed;
            --bg-gradient: linear-gradient(135deg, #f5f3ff 0%, #ede9fe 100%);
        }

        [data-theme="peach"] {
            --primary: #f97316;
            --primary-hover: #ea580c;
            --bg-gradient: linear-gradient(135deg, #fff7ed 0%, #ffedd5 100%);
        }

        [data-theme="mint"] {
            --primary: #10b981;
            --primary-hover: #059669;
            --bg-gradient: linear-gradient(135deg, #ecfdf5 0%, #d1fae5 100%);
        }

        [data-mode="dark"] {
            --bg-gradient: linear-gradient(135deg, #111827 0%, #1f2937 100%);
            --card-bg: #1f2937;
            --text-main: #f9fafb;
            --text-sub: #9ca3af;
        }

        body {
            background: var(--bg-gradient);
            color: var(--text-main);
            min-height: 100vh;
        }

        .custom-card {
            background-color: var(--card-bg);
            color: var(--text-main);
        }
    </style>
</head>
<body class="transition-colors duration-300">

    <!-- ÉCRAN D'AUTHENTIFICATION -->
    <div id="authOverlay" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm p-4">
        <div class="custom-card max-w-md w-full p-8 rounded-2xl shadow-2xl border border-pink-100 dark:border-gray-700">
            <div class="text-center mb-6">
                <span class="text-4xl">💖</span>
                <h1 class="text-2xl font-bold mt-2 bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">N_Sarah Prep Hub</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1" id="authSubtitle">Crée ton compte ou connecte-toi pour accéder à l'EPGE</p>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium mb-1">Ton Pseudo / Nom d'utilisateur</label>
                    <input type="text" id="authUsername" placeholder="Ex: N_Sarah" class="w-full p-3 rounded-xl border border-gray-300 dark:border-gray-600 dark:bg-gray-700 focus:outline-none focus:border-pink-500">
                </div>
                <div>
                    <label class="block text-sm font-medium mb-1">Mot de passe personnel</label>
                    <input type="password" id="authPassword" placeholder="••••••••" class="w-full p-3 rounded-xl border border-gray-300 dark:border-gray-600 dark:bg-gray-700 focus:outline-none focus:border-pink-500">
                </div>
                
                <div class="flex gap-3 pt-2">
                    <button onclick="handleRegister()" class="flex-1 bg-purple-100 dark:bg-gray-700 text-purple-700 dark:text-purple-300 font-semibold py-3 rounded-xl transition text-sm">
                        Créer un compte
                    </button>
                    <button onclick="handleLogin()" class="flex-1 bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3 rounded-xl transition shadow-md text-sm">
                        Se connecter
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- SITE PRINCIPAL -->
    <div id="mainAppContainer" class="hidden">
        <header class="bg-white/80 dark:bg-gray-800/80 backdrop-blur-md shadow-sm sticky top-0 z-40 px-4 py-3 border-b border-pink-100 dark:border-gray-700">
            <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-4">
                <div class="flex items-center space-x-3">
                    <span class="text-2xl">💖</span>
                    <h1 class="text-xl font-bold bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">N_Sarah Prep Hub (EPGE)</h1>
                </div>

                <div class="flex items-center flex-wrap gap-3">
                    <div class="flex items-center space-x-2 bg-pink-50 dark:bg-gray-700 px-3 py-1.5 rounded-full">
                        <span class="text-sm">👤 <strong id="headerUsername" class="text-pink-600 dark:text-pink-400">N_Sarah</strong></span>
                        <button onclick="logout()" class="text-xs text-gray-500 hover:text-red-500 ml-2 font-medium">[Déconnexion]</button>
                    </div>

                    <select id="colorThemeSelect" onchange="changeColorTheme(this.value)" class="text-xs px-2 py-1.5 rounded border border-gray-300 dark:border-gray-600 dark:bg-gray-700 dark:text-white">
                        <option value="girly-pink">🌸 Rose Girly</option>
                        <option value="lavender">💜 Lavande Douce</option>
                        <option value="peach">🍑 Pêche Lumineuse</option>
                        <option value="mint">🌿 Menthe Fraîche</option>
                    </select>

                    <button onclick="toggleDarkMode()" class="p-2 rounded-full bg-gray-200 dark:bg-gray-700 text-sm">
                        🌙/☀️
                    </button>
                </div>
            </div>
        </header>

        <main class="max-w-6xl mx-auto p-4 md:p-6">
            <div id="dashboardView" class="space-y-6">
                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h2 class="text-2xl font-bold mb-2">Bienvenue sur ton espace, <span class="text-pink-500" id="currentUserName">N_Sarah</span> ! ✨</h2>
                    <p class="text-gray-600 dark:text-gray-300 text-sm mb-6">Prépare tes concours EPGE efficacement avec des QCM sur-mesure, des cours détaillés, des malus et un suivi de progression en temps réel.</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="p-4 rounded-xl bg-pink-50 dark:bg-gray-700/50 border border-pink-100 dark:border-gray-600">
                            <h3 class="font-semibold text-pink-600 dark:text-pink-400">📊 Progression globale</h3>
                            <p class="text-2xl font-bold mt-1">15.1 / 20</p>
                            <span class="text-xs text-gray-500">Moyenne générale</span>
                        </div>
                        <div class="p-4 rounded-xl bg-purple-50 dark:bg-gray-700/50 border border-purple-100 dark:border-gray-600">
                            <h3 class="font-semibold text-purple-600 dark:text-purple-400">📝 Tests complétés</h3>
                            <p class="text-2xl font-bold mt-1">6</p>
                            <span class="text-xs text-gray-500">Sessions enregistrées</span>
                        </div>
                        <div class="p-4 rounded-xl bg-amber-50 dark:bg-gray-700/50 border border-amber-100 dark:border-gray-600">
                            <h3 class="font-semibold text-amber-600 dark:text-amber-400">⚡ Établissement</h3>
                            <p class="text-lg font-bold mt-1">EPGE (1ère & 2nde année)</p>
                            <span class="text-xs text-gray-500">Filière ECG & Prépa</span>
                        </div>
                    </div>
                </div>

                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h3 class="text-xl font-bold mb-4">🎯 Lancer une session d'apprentissage</h3>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-sm font-medium mb-1">Matière</label>
                            <select id="subjectSelect" class="w-full p-2.5 rounded-lg border border-gray-300 dark:border-gray-600 dark:bg-gray-700">
                                <option value="Mathématiques">Mathématiques</option>
                                <option value="Économie">Économie (Cours & Exercices)</option>
                                <option value="Géopolitique">Géopolitique</option>
                                <option value="Anglais">Anglais</option>
                                <option value="Français">Français / Culture Générale</option>
                                <option value="Philosophie">Philosophie</option>
                                <option value="Informatique">Informatique</option>
                                <option value="Espagnol">Espagnol</option>
                                <option value="Allemand">Allemand</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-sm font-medium mb-1">Niveau / Filière</label>
                            <select id="levelSelect" class="w-full p-2.5 rounded-lg border border-gray-300 dark:border-gray-600 dark:bg-gray-700">
                                <option value="ECG1">EPGE - 1ère année (ECG1)</option>
                                <option value="ECG2">EPGE - 2nde année (ECG2)</option>
                                <option value="Autre Prépa">Autre filière prépa</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <div>
                            <label class="block text-sm font-medium mb-1">Thème / Leçon spécifique (ex: Périodicité, IS-LM...)</label>
                            <input type="text" id="lessonInput" placeholder="Ex: La périodicité, Algèbre linéaire..." class="w-full p-2.5 rounded-lg border border-gray-300 dark:border-gray-600 dark:bg-gray-700">
                        </div>

                        <div>
                            <label class="block text-sm font-medium mb-1">Nombre de questions (<span id="numQVal">10</span>)</label>
                            <input type="range" id="numQuestionsRange" min="5" max="30" value="10" oninput="document.getElementById('numQVal').innerText=this.value" class="w-full accent-pink-500 mt-3">
                        </div>
                    </div>

                    <div class="flex gap-4">
                        <button onclick="startTest()" class="flex-1 bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3 rounded-xl transition shadow-md">
                            🚀 Lancer le QCM (Chrono 30 min)
                        </button>
                        <button onclick="viewTheory()" class="px-6 bg-purple-100 dark:bg-gray-700 text-purple-700 dark:text-purple-300 font-semibold py-3 rounded-xl transition">
                            📖 Fiche de Cours & Résumé
                        </button>
                    </div>
                </div>

                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h3 class="text-xl font-bold mb-4">📈 Évolution de ta progression</h3>
                    <div class="h-64">
                        <canvas id="progressChart"></canvas>
                    </div>
                </div>
            </div>

            <div id="testView" class="hidden space-y-6">
                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <div class="flex justify-between items-center mb-6 border-b pb-4 dark:border-gray-700">
                        <div>
                            <span id="testSubjectBadge" class="px-3 py-1 bg-pink-100 text-pink-700 text-xs font-semibold rounded-full">Maths</span>
                            <h2 class="text-xl font-bold mt-2" id="testTitle">Question 1 sur 10</h2>
                        </div>
                        <div class="text-right">
                            <span class="text-xs text-gray-500 block">Temps restant</span>
                            <span id="timerDisplay" class="text-xl font-bold text-pink-500">30:00</span>
                        </div>
                    </div>

                    <div id="questionContainer" class="space-y-4 mb-6"></div>

                    <div class="flex justify-end">
                        <button id="nextQuestionBtn" onclick="nextQuestion()" class="bg-pink-500 hover:bg-pink-600 text-white px-6 py-2.5 rounded-xl font-semibold transition" disabled>
                            Valider & Continuer ➔
                        </button>
                    </div>
                </div>
            </div>

            <div id="resultView" class="hidden space-y-6">
                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700 text-center">
                    <h2 class="text-3xl font-bold mb-2">🎉 Test Terminé !</h2>
                    <p class="text-gray-600 dark:text-gray-300 mb-4">Voici ton bilan personnalisé pour cette session.</p>
                    
                    <div class="inline-block p-6 rounded-2xl bg-pink-50 dark:bg-gray-700/50 border border-pink-100 mb-6">
                        <span class="text-sm text-gray-500 block">Note finale</span>
                        <span class="text-4xl font-extrabold text-pink-600 dark:text-pink-400" id="finalScoreDisplay">14.5 / 20</span>
                    </div>

                    <div class="text-left space-y-4 mb-6">
                        <h3 class="font-bold text-lg">💡 Corrections & Tips personnalisés :</h3>
                        <div id="correctionContainer" class="space-y-3"></div>
                    </div>

                    <button onclick="returnHome()" class="bg-pink-500 hover:bg-pink-600 text-white px-8 py-3 rounded-xl font-semibold transition">
                        🏠 Revenir au Tableau de Bord
                    </button>
                </div>
            </div>
        </main>
    </div>

    <script>
        let currentUser = null;
        let currentTheme = "girly-pink";
        let currentMode = "light";
        let currentTest = { subject: "", lesson: "", questions: [], currentIndex: 0, userAnswers: [], score: 0 };
        let timerInterval = null;
        let timeLeft = 1800;
        let progressChartInstance = null;

        window.addEventListener('DOMContentLoaded', () => {
            const savedUser = localStorage.getItem('epge_current_user');
            if(savedUser) {
                currentUser = savedUser;
                initUserSession();
            }
        });

        function handleRegister() {
            const username = document.getElementById('authUsername').value.trim();
            const pass = document.getElementById('authPassword').value.trim();
            
            if(!username || !pass) {
                alert("Veuillez entrer un pseudo et un mot de passe valide.");
                return;
            }

            let users = JSON.parse(localStorage.getItem('epge_users') || '{}');
            if(users[username]) {
                alert("Ce compte existe déjà. Veuillez cliquer sur 'Se connecter' !");
                return;
            }

            users[username] = pass;
            localStorage.setItem('epge_users', JSON.stringify(users));
            
            currentUser = username;
            localStorage.setItem('epge_current_user', currentUser);
            initUserSession();
        }

        function handleLogin() {
            const username = document.getElementById('authUsername').value.trim();
            const pass = document.getElementById('authPassword').value.trim();

            if(!username || !pass) {
                alert("Veuillez remplir tous les champs.");
                return;
            }

            let users = JSON.parse(localStorage.getItem('epge_users') || '{}');
            
            if(users[username]) {
                if(users[username] === pass) {
                    currentUser = username;
                    localStorage.setItem('epge_current_user', currentUser);
                    initUserSession();
                } else {
                    alert("Mot de passe incorrect.");
                }
            } else {
                // Si l'utilisateur n'a pas cliqué sur créer un compte mais tape ses infos, on l'inscrit automatiquement pour lui faciliter la vie
                users[username] = pass;
                localStorage.setItem('epge_users', JSON.stringify(users));
                currentUser = username;
                localStorage.setItem('epge_current_user', currentUser);
                initUserSession();
            }
        }

        function initUserSession() {
            document.getElementById('authOverlay').classList.add('hidden');
            document.getElementById('mainAppContainer').classList.remove('hidden');
            document.getElementById('headerUsername').innerText = currentUser;
            document.getElementById('currentUserName').innerText = currentUser;
            loadUserStats();
        }

        function logout() {
            localStorage.removeItem('epge_current_user');
            location.reload();
        }

        function changeColorTheme(theme) {
            currentTheme = theme;
            document.documentElement.setAttribute('data-theme', theme);
        }

        function toggleDarkMode() {
            currentMode = currentMode === "light" ? "dark" : "light";
            document.documentElement.setAttribute('data-mode', currentMode);
        }

        function initChart() {
            const ctx = document.getElementById('progressChart').getContext('2d');
            if(progressChartInstance) progressChartInstance.destroy();
            
            progressChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Test 1', 'Test 2', 'Test 3', 'Test 4', 'Dernier test'],
                    datasets: [{
                        label: 'Notes (/20)',
                        data: [12, 14, 13.5, 16, 17],
                        borderColor: '#ec4899',
                        backgroundColor: 'rgba(236, 72, 153, 0.1)',
                        fill: true,
                        tension: 0.3
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: { beginAtZero: true, max: 20 }
                    }
                }
            });
        }

        function loadUserStats() {
            initChart();
        }

        function startTest() {
            const subject = document.getElementById("subjectSelect").value;
            const lesson = document.getElementById("lessonInput").value || "Généralités";
            const numQ = parseInt(document.getElementById("numQuestionsRange").value);
            
            currentTest = {
                subject,
                lesson,
                questions: generateQuestions(subject, lesson, numQ),
                currentIndex: 0,
                userAnswers: [],
                score: 0
            };

            document.getElementById("dashboardView").classList.add("hidden");
            do

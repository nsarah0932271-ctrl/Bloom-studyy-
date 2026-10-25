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
        
        /* Thèmes de couleurs et modes */
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

    <!-- ÉCRAN D'AUTHENTIFICATION (Affiché si non connecté) -->
    <div id="authOverlay" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm p-4">
        <div class="custom-card max-w-md w-full p-8 rounded-2xl shadow-2xl border border-pink-100 dark:border-gray-700">
            <div class="text-center mb-6">
                <span class="text-4xl">💖</span>
                <h1 class="text-2xl font-bold mt-2 bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">N_Sarah Prep Hub</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">Espace Prépa EPGE - Connexion requise</p>
            </div>

            <!-- Formulaire de Connexion / Inscription -->
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
                    <button onclick="handleLogin()" class="flex-1 bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3 rounded-xl transition shadow-md">
                        Se connecter
                    </button>
                    <button onclick="handleRegister()" class="flex-1 bg-purple-100 dark:bg-gray-700 text-purple-700 dark:text-purple-300 font-semibold py-3 rounded-xl transition">
                        Créer un compte
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- SITE PRINCIPAL (Masqué tant que non connecté) -->
    <div id="mainAppContainer" class="hidden">
        <!-- BARRE DE CONFIGURATION ET UTILISATEUR -->
        <header class="bg-white/80 dark:bg-gray-800/80 backdrop-blur-md shadow-sm sticky top-0 z-40 px-4 py-3 border-b border-pink-100 dark:border-gray-700">
            <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-4">
                <div class="flex items-center space-x-3">
                    <span class="text-2xl">💖</span>
                    <h1 class="text-xl font-bold bg-gradient-to-r from-pink-500 to-purple-500 bg-clip-text text-transparent">N_Sarah Prep Hub (EPGE)</h1>
                </div>

                <!-- Paramètres & Compte connecté -->
                <div class="flex items-center flex-wrap gap-3">
                    <div class="flex items-center space-x-2 bg-pink-50 dark:bg-gray-700 px-3 py-1.5 rounded-full">
                        <span class="text-sm">👤 <strong id="headerUsername" class="text-pink-600 dark:text-pink-400">N_Sarah</strong></span>
                        <button onclick="logout()" class="text-xs text-gray-500 hover:text-red-500 ml-2 font-medium" title="Se déconnecter">[Déconnexion]</button>
                    </div>

                    <!-- Sélecteur de Thème Couleur -->
                    <select id="colorThemeSelect" onchange="changeColorTheme(this.value)" class="text-xs px-2 py-1.5 rounded border border-gray-300 dark:border-gray-600 dark:bg-gray-700 dark:text-white">
                        <option value="girly-pink">🌸 Rose Girly</option>
                        <option value="lavender">💜 Lavande Douce</option>
                        <option value="peach">🍑 Pêche Lumineuse</option>
                        <option value="mint">🌿 Menthe Fraîche</option>
                    </select>

                    <!-- Sélecteur Mode Clair / Sombre -->
                    <button onclick="toggleDarkMode()" class="p-2 rounded-full bg-gray-200 dark:bg-gray-700 text-sm" title="Basculer Mode Clair/Sombre">
                        🌙/☀️
                    </button>
                </div>
            </div>
        </header>

        <!-- CONTENU PRINCIPAL -->
        <main class="max-w-6xl mx-auto p-4 md:p-6">

            <!-- VUE ACCUEIL / TABLEAU DE BORD -->
            <div id="dashboardView" class="space-y-6">
                <div class="custom-card p-6 rounded-2xl shadow-lg border border-pink-100 dark:border-gray-700">
                    <h2 class="text-2xl font-bold mb-2">Bienvenue sur ton espace, <span class="text-pink-500" id="currentUserName">N_Sarah</span> ! ✨</h2>
                    <p class="text-gray-600 dark:text-gray-300 text-sm mb-6">Prépare tes concours EPGE efficacement avec des QCM sur-mesure, des cours détaillés, des malus et un suivi de progression en temps réel.</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="p-4 rounded-xl bg-pink-50 dark:bg-gray-700/50 border border-pink-100 dark:border-gray-600">
                            <h3 class="font-semibold text-pink-600 dark:text-pink-400">📊 Progression globale</h3>
                            <p class="text-2xl font-bold mt-1" id="statAvgScore">-- / 20</p>
                            <span class="text-xs text-gray-500">Moyenne générale</span>
                        </div>
                        <div class="p-4 rounded-xl bg-purple-50 dark:bg-gray-700/50 border border-purple-100 dark:border-gray-600">
                            <h3 class="font-semibold text-purple-600 dark:text-purple-400">📝 Tests complétés</h3>
                            <p class="text-2xl font-bold mt-1" id="statTestsCount">0</p>
                            <span class="text-xs text-gray-500">Sessions enregistrées</span>
                        </div>
                        <div class="p-4 rounded-xl bg-amber-50 dark:bg-gray-700/50 border border-amber-100 dark:border-gray-600">
                            <h3 class="font-semibold text-amber-600 dark:text-amber-400">⚡ Établissement</h3>
                            <p class="text-lg font-bold mt-1">EPGE (1ère & 2nde année)</p>
                            <span class="text-xs text-gray-500">Filière ECG & Prépa</span>
                        </div>
                    </div>
                </div>

                <!-- CONFIGURATEUR DE TEST / COURS -->
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
                            <select id="levelSelect" class
                            

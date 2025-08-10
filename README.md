<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test de Profil Psychologique</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .scale-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            padding: 0 5px;
        }
        .scale-container label {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            font-size: 0.75rem;
            color: #6b7280;
            cursor: pointer;
        }
        .scale-container input[type="radio"] {
            margin-bottom: 0.25rem;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <div class="container mx-auto max-w-3xl p-4 sm:p-8">
        <header class="text-center mb-8">
            <h1 class="text-3xl sm:text-4xl font-bold text-gray-900">Test de Profil Psychologique</h1>
            <p class="mt-2 text-lg text-gray-600">Découvrez vos traits de personnalité dominants.</p>
        </header>

        <main id="test-container" class="bg-white p-6 sm:p-8 rounded-xl shadow-md">
            <div id="instructions" class="mb-8">
                <h2 class="text-xl font-semibold mb-3 text-gray-800">Instructions</h2>
                <p class="text-gray-700">Pour chaque affirmation ci-dessous, indiquez à quel point elle vous correspond. Il n'y a pas de bonnes ou de mauvaises réponses. Soyez honnête pour obtenir le profil le plus précis.</p>
            </div>

            <form id="quiz-form">
                <div id="questions-container" class="space-y-8">
                    <!-- Les questions seront injectées ici par JavaScript -->
                </div>
                <div class="mt-10 text-center">
                    <button type="submit" class="bg-blue-600 text-white font-bold py-3 px-8 rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300">
                        Voir mon profil
                    </button>
                </div>
            </form>
        </main>

        <div id="results-container" class="hidden mt-10 bg-white p-6 sm:p-8 rounded-xl shadow-md">
             <h2 class="text-2xl sm:text-3xl font-bold text-center mb-6 text-gray-900">Votre Profil de Personnalité</h2>
             <div id="results-content" class="space-y-6">
                <!-- Les résultats seront injectés ici -->
             </div>
             <div class="text-center mt-8">
                <button onclick="resetTest()" class="bg-gray-200 text-gray-800 font-semibold py-2 px-6 rounded-lg hover:bg-gray-300 transition duration-300">
                    Refaire le test
                </button>
             </div>
        </div>
        
        <footer class="text-center mt-12 text-sm text-gray-500">
            <p>Ce test est un outil de découverte et ne remplace pas un diagnostic psychologique professionnel.</p>
        </footer>

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            // --- Définition des questions ---
            const questions = [
                // Conscienciosité (organisation, fiabilité)
                { text: "Je suis une personne méticuleuse et soucieuse du détail.", trait: 'conscientiousness', score: 1 },
                { text: "Je planifie mes tâches à l'avance pour respecter les délais.", trait: 'conscientiousness', score: 1 },
                { text: "J'ai tendance à laisser les choses en désordre.", trait: 'conscientiousness', score: -1 },
                { text: "Je suis discipliné(e) et j'accomplis mes tâches sans qu'on ait à me le rappeler.", trait: 'conscientiousness', score: 1 },

                // Agréabilité (travail d'équipe, empathie)
                { text: "La collaboration est pour moi la clé du succès dans un projet.", trait: 'agreeableness', score: 1 },
                { text: "Je m'intéresse sincèrement aux problèmes des autres.", trait: 'agreeableness', score: 1 },
                { text: "J'ai tendance à imposer mes idées dans un groupe.", trait: 'agreeableness', score: -1 },
                { text: "Il est important pour moi que tout le monde se sente inclus et écouté.", trait: 'agreeableness', score: 1 },

                // Stabilité Émotionnelle (gestion du stress, calme)
                { text: "Je reste calme et serein(e) même dans les situations stressantes.", trait: 'emotionalStability', score: 1 },
                { text: "Je m'inquiète souvent pour des choses sans grande importance.", trait: 'emotionalStability', score: -1 },
                { text: "Je suis capable de gérer la critique constructive sans me sentir personnellement attaqué(e).", trait: 'emotionalStability', score: 1 },
                { text: "Mon humeur est généralement stable et prévisible.", trait: 'emotionalStability', score: 1 },

                // Extraversion (sociabilité, leadership)
                { text: "Je suis à l'aise pour prendre la parole en public ou animer une réunion.", trait: 'extraversion', score: 1 },
                { text: "Je préfère travailler seul(e) plutôt qu'en équipe.", trait: 'extraversion', score: -1 },
                { text: "Je prends facilement l'initiative dans les discussions de groupe.", trait: 'extraversion', score: 1 },
                { text: "Je me sens plein(e) d'énergie après avoir interagi avec beaucoup de gens.", trait: 'extraversion', score: 1 },

                // Ouverture (curiosité, adaptabilité)
                { text: "Le changement et les nouvelles expériences me stimulent.", trait: 'openness', score: 1 },
                { text: "Je préfère suivre des routines et des méthodes qui ont fait leurs preuves.", trait: 'openness', score: -1 },
                { text: "J'aime explorer des idées abstraites et des concepts complexes.", trait: 'openness', score: 1 },
                { text: "Face à un problème inattendu, je trouve rapidement une solution créative.", trait: 'openness', score: 1 },
            ];

            // --- Génération des questions dans le HTML ---
            const questionsContainer = document.getElementById('questions-container');
            questions.forEach((q, index) => {
                const questionElement = document.createElement('div');
                questionElement.className = 'question-block border-t border-gray-200 pt-6';
                questionElement.innerHTML = `
                    <p class="font-semibold text-lg mb-4 text-gray-800">${index + 1}. ${q.text}</p>
                    <div class="scale-container">
                        <label>Pas du tout d'accord<input type="radio" name="q${index}" value="1" required></label>
                        <label>Pas d'accord<input type="radio" name="q${index}" value="2"></label>
                        <label>Neutre<input type="radio" name="q${index}" value="3"></label>
                        <label>D'accord<input type="radio" name="q${index}" value="4"></label>
                        <label>Tout à fait d'accord<input type="radio" name="q${index}" value="5"></label>
                    </div>
                `;
                questionsContainer.appendChild(questionElement);
            });

            // --- Gestion de la soumission du formulaire ---
            const form = document.getElementById('quiz-form');
            form.addEventListener('submit', function (event) {
                event.preventDefault();
                
                const scores = {
                    conscientiousness: { total: 0, count: 0 },
                    agreeableness: { total: 0, count: 0 },
                    emotionalStability: { total: 0, count: 0 },
                    extraversion: { total: 0, count: 0 },
                    openness: { total: 0, count: 0 }
                };

                // Calcul des scores
                questions.forEach((q, index) => {
                    const selectedValue = document.querySelector(`input[name="q${index}"]:checked`);
                    if (selectedValue) {
                        let value = parseInt(selectedValue.value);
                        if (q.score === -1) {
                            value = 6 - value; // Inverser le score pour les questions négatives
                        }
                        scores[q.trait].total += value;
                        scores[q.trait].count++;
                    }
                });

                // Calcul des pourcentages
                const results = {};
                for (const trait in scores) {
                    const maxScore = scores[trait].count * 5;
                    const minScore = scores[trait].count * 1;
                    results[trait] = Math.round(((scores[trait].total - minScore) / (maxScore - minScore)) * 100);
                }

                displayResults(results);
            });

            // --- Affichage des résultats ---
            const traitDescriptions = {
                conscientiousness: {
                    title: "Conscienciosité (Organisation et Fiabilité)",
                    low: "Vous avez tendance à être spontané(e) et flexible. Vous préférez vous adapter aux situations plutôt que de suivre un plan strict, ce qui peut être un atout dans des environnements changeants.",
                    medium: "Vous êtes capable de planifier et de vous organiser lorsque c'est nécessaire, tout en gardant une certaine flexibilité. Vous trouvez un bon équilibre entre structure et spontanéité.",
                    high: "Vous êtes une personne très organisée, fiable et disciplinée. Vous prenez vos responsabilités au sérieux et vous êtes méticuleux(se) dans votre travail, ce qui inspire confiance."
                },
                agreeableness: {
                    title: "Agréabilité (Coopération et Esprit d'équipe)",
                    low: "Vous êtes direct(e) et n'hésitez pas à défendre vos opinions, même si cela crée un débat. Vous privilégiez l'efficacité et la vérité à l'harmonie à tout prix.",
                    medium: "Vous savez collaborer et faire des compromis, mais vous n'hésitez pas à exprimer votre point de vue lorsque c'est important. Vous équilibrez bien coopération et affirmation de soi.",
                    high: "Vous êtes une personne coopérative, empathique et bienveillante. Vous excellez dans le travail d'équipe et vous vous souciez sincèrement de maintenir de bonnes relations avec les autres."
                },
                emotionalStability: {
                    title: "Stabilité Émotionnelle (Gestion du Stress et Calme)",
                    low: "Vous êtes sensible et réactif/réactive aux événements. Vous ressentez les émotions intensément, ce qui peut être une source de créativité mais aussi de stress.",
                    medium: "Vous gérez le stress de manière équilibrée. Vous pouvez ressentir de la pression, mais vous avez les ressources pour y faire face sans vous laisser submerger.",
                    high: "Vous êtes d'un naturel calme, résilient(e) et stable. Vous gérez très bien la pression et le stress, ce qui vous permet de rester concentré(e) et efficace dans les situations difficiles."
                },
                extraversion: {
                    title: "Extraversion (Sociabilité et Leadership)",
                    low: "Vous êtes plutôt réservé(e) et introspectif/ve. Vous préférez les interactions en petit groupe et vous avez besoin de temps seul(e) pour recharger vos batteries. Vous êtes un(e) excellent(e) auditeur/auditrice.",
                    medium: "Vous appréciez à la fois les moments de sociabilité et les moments de calme. Vous êtes à l'aise dans diverses situations sociales sans ressentir le besoin constant d'être entouré(e).",
                    high: "Vous êtes sociable, énergique et assertif/ve. Vous tirez votre énergie des interactions sociales et vous êtes à l'aise pour prendre les devants et animer un groupe."
                },
                openness: {
                    title: "Ouverture (Créativité et Adaptabilité)",
                    low: "Vous êtes pragmatique et préférez les approches concrètes et éprouvées. Vous appréciez la tradition et la stabilité, et vous excellez dans l'optimisation des systèmes existants.",
                    medium: "Vous êtes ouvert(e) aux nouvelles idées tout en restant ancré(e) dans la réalité. Vous appréciez l'innovation lorsqu'elle est justifiée et pratique.",
                    high: "Vous êtes très curieux(se), créatif/ve et imaginatif/ve. Vous aimez explorer de nouvelles idées, remettre en question les conventions et vous vous adaptez facilement au changement."
                }
            };
            
            function displayResults(results) {
                const resultsContent = document.getElementById('results-content');
                resultsContent.innerHTML = '';

                for (const trait in results) {
                    const score = results[trait];
                    const description = traitDescriptions[trait];
                    let analysisText;

                    if (score < 40) {
                        analysisText = description.low;
                    } else if (score <= 60) {
                        analysisText = description.medium;
                    } else {
                        analysisText = description.high;
                    }

                    const resultElement = document.createElement('div');
                    resultElement.className = 'result-item';
                    resultElement.innerHTML = `
                        <h3 class="font-semibold text-lg mb-2 text-blue-700">${description.title}</h3>
                        <div class="w-full bg-gray-200 rounded-full h-2.5 mb-2">
                            <div class="bg-blue-600 h-2.5 rounded-full" style="width: ${score}%"></div>
                        </div>
                        <p class="text-gray-700">${analysisText}</p>
                    `;
                    resultsContent.appendChild(resultElement);
                }

                document.getElementById('test-container').classList.add('hidden');
                document.getElementById('results-container').classList.remove('hidden');
                window.scrollTo(0, 0);
            }

            window.resetTest = function() {
                document.getElementById('quiz-form').reset();
                document.getElementById('results-container').classList.add('hidden');
                document.getElementById('test-container').classList.remove('hidden');
                 window.scrollTo(0, 0);
            }

        });
    </script>
</body>
</html>


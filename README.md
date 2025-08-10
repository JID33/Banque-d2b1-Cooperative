<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test de Profil Psychologique Professionnel</title>
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
            <h1 class="text-3xl sm:text-4xl font-bold text-gray-900">Test de Profil Psychologique Professionnel</h1>
            <p class="mt-2 text-lg text-gray-600">Découvrez vos traits de personnalité et leur implication professionnelle.</p>
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
                        Voir mon profil et mon analyse
                    </button>
                </div>
            </form>
        </main>

        <div id="results-container" class="hidden mt-10">
             <div class="bg-white p-6 sm:p-8 rounded-xl shadow-md">
                <h2 class="text-2xl sm:text-3xl font-bold text-center mb-6 text-gray-900">Votre Profil de Personnalité</h2>
                <div id="results-content" class="space-y-6">
                    <!-- Les résultats du profil seront injectés ici -->
                </div>
             </div>

             <div class="mt-8 bg-white p-6 sm:p-8 rounded-xl shadow-md">
                <h2 class="text-2xl sm:text-3xl font-bold text-center mb-6 text-gray-900">Analyse Professionnelle et Points de Vigilance</h2>
                <div id="professional-analysis" class="space-y-4 text-gray-700">
                    <!-- L'analyse professionnelle sera injectée ici -->
                </div>
             </div>

             <div class="text-center mt-8">
                <button onclick="resetTest()" class="bg-gray-200 text-gray-800 font-semibold py-2 px-6 rounded-lg hover:bg-gray-300 transition duration-300">
                    Refaire le test
                </button>
             </div>
        </div>
        
        <footer class="text-center mt-12 text-sm text-gray-500">
            <p>Ce test est un outil de découverte et ne remplace pas un diagnostic psychologique ou une évaluation professionnelle complète.</p>
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

                questions.forEach((q, index) => {
                    const selectedValue = document.querySelector(`input[name="q${index}"]:checked`);
                    if (selectedValue) {
                        let value = parseInt(selectedValue.value);
                        if (q.score === -1) {
                            value = 6 - value;
                        }
                        scores[q.trait].total += value;
                        scores[q.trait].count++;
                    }
                });

                const results = {};
                for (const trait in scores) {
                    const maxScore = scores[trait].count * 5;
                    const minScore = scores[trait].count * 1;
                    results[trait] = Math.round(((scores[trait].total - minScore) / (maxScore - minScore)) * 100);
                }

                displayResults(results);
                displayProfessionalAnalysis(results);
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

            // --- NOUVELLE FONCTION : Analyse Professionnelle ---
            function displayProfessionalAnalysis(scores) {
                const analysisContainer = document.getElementById('professional-analysis');
                let strengths = [];
                let developments = [];
                let environment = [];

                // Analyse des forces
                if (scores.conscientiousness > 70) strengths.push("une <strong>grande fiabilité</strong> et un <strong>sens de l'organisation</strong>, assurant un travail de qualité et le respect des délais.");
                if (scores.emotionalStability > 70) strengths.push("une <strong>excellente gestion du stress</strong>, vous permettant de rester performant(e) et lucide dans les situations de haute pression.");
                if (scores.agreeableness > 70) strengths.push("un <strong>fort esprit d'équipe</strong> et des <strong>compétences relationnelles</strong> qui favorisent un environnement de travail harmonieux et collaboratif.");
                if (scores.extraversion > 70) strengths.push("une <strong>aisance à communiquer</strong> et à prendre des initiatives, ce qui est un moteur pour l'équipe et un atout en leadership.");
                if (scores.openness > 70) strengths.push("une <strong>grande créativité</strong> et une <strong>forte capacité d'adaptation</strong>, vous rendant apte à innover et à gérer le changement.");

                // Analyse des axes de développement
                if (scores.conscientiousness < 40) developments.push("La flexibilité est une force, mais un cadre plus structuré pour la gestion des priorités pourrait améliorer l'efficacité sur les projets à long terme.");
                if (scores.emotionalStability < 40) developments.push("Votre sensibilité vous permet de bien percevoir votre environnement. Développer des techniques de gestion des émotions pourrait aider à canaliser cette énergie de manière constructive face au stress.");
                if (scores.agreeableness < 40) developments.push("Votre capacité à défendre vos idées est précieuse. L'associer à des techniques d'écoute active peut renforcer votre impact et la cohésion d'équipe.");
                if (scores.extraversion < 40) developments.push("Votre concentration en autonomie est un atout majeur. Dans les projets d'équipe, une communication proactive sur vos avancées peut être un point d'attention pour assurer l'alignement de tous.");
                if (scores.openness < 40) developments.push("Votre pragmatisme assure la stabilité. S'ouvrir à des approches nouvelles, même à petite échelle, pourrait révéler des opportunités d'optimisation inattendues.");

                // Analyse de l'environnement de travail idéal
                if (scores.openness > 65 && scores.extraversion > 65) environment.push("dynamiques, innovants et sociaux (ex: start-up, marketing, gestion de projet).");
                if (scores.conscientiousness > 65 && scores.emotionalStability > 65) environment.push("structurés, stables et exigeant de la précision (ex: finance, administration, ingénierie qualité).");
                if (scores.agreeableness > 65 && scores.extraversion < 45) environment.push("collaboratifs et centrés sur le service ou le soin (ex: support client, ressources humaines, santé).");
                if (scores.openness < 45 && scores.conscientiousness > 65) environment.push("où les procédures sont claires et la qualité prime (ex: production, logistique, conformité).");
                 if (environment.length === 0) environment.push("polyvalents, où vous pouvez équilibrer autonomie et collaboration, routine et nouveauté.");

                let html = `
                    <div>
                        <h4 class="font-semibold text-lg text-green-700 mb-2">Forces Clés pour une Équipe</h4>
                        ${strengths.length > 0 ? `<ul class="list-disc list-inside space-y-1">${strengths.map(s => `<li>${s}</li>`).join('')}</ul>` : "<p>Votre profil équilibré vous rend polyvalent(e) et adaptable à de nombreux contextes.</p>"}
                    </div>
                    <div class="border-t border-gray-200 pt-4">
                        <h4 class="font-semibold text-lg text-orange-700 mb-2">Axes de Développement Potentiels</h4>
                         ${developments.length > 0 ? `<ul class="list-disc list-inside space-y-1">${developments.map(d => `<li>${d}</li>`).join('')}</ul>` : "<p>Votre profil ne présente pas d'axe de développement majeur, indiquant une bonne balance dans vos traits de personnalité.</p>"}
                    </div>
                    <div class="border-t border-gray-200 pt-4">
                        <h4 class="font-semibold text-lg text-indigo-700 mb-2">Ersonne très organisée, fiable et disciplinée. Vous prenez vos responsabilités au sérieux et vous êtes méticuleux(se) dans votre travail, ce qui inspire confiance."
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


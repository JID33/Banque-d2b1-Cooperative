# Banque-d2b1-Cooperative
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Coopérative D2B1 Solidaire</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      background: #f4faff;
      color: #0a2540;
    }
    header {
      background-color: #d0ecff;
      text-align: center;
      padding: 30px 20px;
    }
    header h1 {
      margin: 0;
      font-size: 2em;
      color: #0a2540;
    }
    header p {
      font-size: 1.1em;
      margin-top: 10px;
    }
    .section {
      padding: 40px 20px;
      text-align: center;
    }
    .section h2 {
      font-size: 1.8em;
      margin-bottom: 30px;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      max-width: 1000px;
      margin: 0 auto;
    }
    .card {
      background: white;
      padding: 20px;
      border: 1px solid #cbe4f9;
      border-radius: 12px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.05);
    }
    .card h3 {
      margin-top: 10px;
    }
    .card p {
      font-size: 0.95em;
      color: #333;
    }
    .button {
      display: inline-block;
      padding: 10px 20px;
      background-color: #0077cc;
      color: white;
      border-radius: 8px;
      text-decoration: none;
      margin-top: 10px;
    }
    .faq {
      max-width: 800px;
      margin: 0 auto;
      text-align: left;
    }
    .faq ul {
      list-style-type: circle;
      padding-left: 20px;
    }
    footer {
      background-color: #e0f0ff;
      text-align: center;
      padding: 20px;
      font-size: 0.9em;
    }
    footer a {
      margin: 0 10px;
      text-decoration: none;
      color: #0077cc;
    }
  </style>
</head>
<body>

<header>
  <h1>Coopérative D2B1 Solidaire</h1>
  <p>Ensemble, nous bâtissons notre avenir.<br>
  Une coopérative solidaire pour le financement local, par la communauté et pour la communauté.</p>
</header>

<section class="section">
  <h2>Nos Services</h2>
  <div class="grid">
    <div class="card">
      <h3>💸 Épargne solidaire</h3>
      <p>Cotisation régulière mensuelle pour les membres.</p>
    </div>
    <div class="card">
      <h3>🔁 Crédit rotatif</h3>
      <p>Prêts tournants entre membres selon un calendrier.</p>
    </div>
    <div class="card">
      <h3>🛠️ Financement de projets</h3>
      <p>Demande de micro-financement pour projets locaux.</p>
    </div>
    <div class="card">
      <h3>📊 Participation aux décisions</h3>
      <p>Assemblées virtuelles ou sondages communautaires.</p>
    </div>
    <div class="card">
      <h3>🔐 Espace Membre Sécurisé</h3>
      <a href="#" class="button">Connexion</a>
    </div>
    <div class="card">
      <h3>🧑‍🤝‍🧑 Devenir Membre</h3>
      <a href="#" class="button">Rejoindre</a>
    </div>
    <div class="card">
      <h3>📋 Projets financés</h3>
      <a href="#" class="button">Voir</a>
    </div>
    <div class="card">
      <h3>📄 Documents et règlements</h3>
      <a href="#" class="button">Lire</a>
    </div>
  </div>
</section>

<section class="section">
  <h2>FAQ Coopérative</h2>
  <div class="faq">
    <ul>
      <li>Qui peut devenir membre ?</li>
      <li>Comment les rotations fonctionnent-elles ?</li>
      <li>Que se passe-t-il si un membre ne paie pas ?</li>
      <li>Peut-on quitter la coopérative ?</li>
      <li>Comment les décisions sont-elles prises ?</li>
    </ul>
  </div>
</section>

<footer>
  📩 contact@d2b1solidaire.fr |
  <a href="#">Rejoindre la coopérative</a> |
  <a href="#">Voir les règles</a>
</footer>

</body>
</html>

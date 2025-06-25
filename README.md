<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Banque-d2b1-Cooperative</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f7fa;
      margin: 0;
      padding: 20px;
      color: #333;
    }
    .section {
      margin-bottom: 30px;
    }
    .title {
      font-size: 24px;
      font-weight: bold;
      color: #006699;
      margin-bottom: 10px;
    }
    .service, .faq-item {
      margin-bottom: 15px;
    }
    .actions a {
      display: inline-block;
      margin: 5px 10px 5px 0;
      padding: 10px 15px;
      background: #006699;
      color: white;
      text-decoration: none;
      border-radius: 5px;
    }
    footer {
      margin-top: 30px;
      font-size: 0.9em;
      color: #666;
    }
    .download-btn {
      margin-top: 40px;
      padding: 12px 20px;
      background-color: #006699;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }
  </style>
</head>
<body>

  <div class="section title">Coopérative D2B1 Solidaire</div>
  <div class="section">
    Ensemble, nous bâtissons notre avenir.<br />
    Une coopérative solidaire pour le financement local, par la communauté et pour la communauté.
  </div>

  <div class="section title">Nos Services</div>
  <div class="section">
    💸 Épargne solidaire<br />
    Cotisation régulière mensuelle pour les membres.<br /><br />

    🔁 Crédit rotatif<br />
    Prêts tournants entre membres selon un calendrier.<br /><br />

    🛠️ Financement de projets<br />
    Demande de micro-financement pour projets locaux.<br /><br />

    📊 Participation aux décisions<br />
    Assemblées virtuelles ou sondages communautaires.
  </div>

  <div class="section title">🔐 Espace Membre Sécurisé</div>
  <div class="actions">
    <a href="#">Connexion</a>
    <a href="#">🧑‍🤝‍🧑 Devenir Membre</a>
    <a href="#">📋 Projets financés</a>
    <a href="#">📄 Documents et règlements</a>
  </div>

  <div class="section title">FAQ Coopérative</div>
  <div class="faq-item">Qui peut devenir membre ?</div>
  <div>Toute personne partageant nos valeurs solidaires et prête à s'engager.</div>

  <div class="faq-item">Comment les rotations fonctionnent-elles ?</div>
  <div>Un calendrier de tirage est défini selon les contributions et priorités.</div>

  <div class="faq-item">Que se passe-t-il si un membre ne paie pas ?</div>
  <div>Des mesures de médiation sont mises en place, voire exclusion après plusieurs rappels.</div>

  <div class="faq-item">Peut-on quitter la coopérative ?</div>
  <div>Oui, selon les règles établies dans le règlement intérieur.</div>

  <div class="faq-item">Comment les décisions sont-elles prises ?</div>
  <div>Par sondage, vote en ligne ou lors des assemblées générales.</div>

  <footer>
    📩 contact@d2b1solidaire.fr |
    <a href="#">Rejoindre la coopérative</a> |
    <a href="#">Voir les règles</a>
  </footer>

  <button class="download-btn" onclick="downloadHTML()">📥 Télécharger cette page</button>

  <script>
    function downloadHTML() {
      const htmlContent = document.documentElement.outerHTML;
      const blob = new Blob([htmlContent], { type: "text/html" });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = "cooperative-d2b1.html";
      a.click();
      URL.revokeObjectURL(url);
    }
  </script>

</body>
</html>

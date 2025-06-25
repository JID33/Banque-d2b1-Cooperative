
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Coopérative D2B1 Solidaire</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f8fbff;
      margin: 0;
      padding: 0;
      color: #333;
    }
    header {
      background: #cceeff;
      padding: 30px 20px;
      text-align: center;
    }
    header h1 {
      margin: 0;
      color: #003366;
    }
    header p {
      margin: 5px 0;
      font-size: 18px;
    }
    section {
      padding: 20px;
      max-width: 960px;
      margin: auto;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
    }
    .card {
      border: 1px solid #cce0ff;
      border-radius: 10px;
      padding: 15px;
      background: #fff;
      text-align: center;
    }
    h2 {
      color: #003366;
      margin-bottom: 10px;
    }
    .btn {
      display: inline-block;
      padding: 10px 20px;
      margin: 10px 5px;
      background-color: #0066cc;
      color: white;
      border: none;
      border-radius: 5px;
      text-decoration: none;
      cursor: pointer;
    }
    form {
      display: grid;
      gap: 10px;
      background: #eef6ff;
      padding: 20px;
      border-radius: 8px;
      margin-top: 30px;
    }
    input {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    table {
      margin-top: 20px;
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: left;
    }
    footer {
      margin-top: 30px;
      text-align: center;
      font-size: 0.9em;
      padding: 20px;
      background: #e6f2ff;
    }
  </style>
</head>
<body>

<header>
  <h1>Coopérative D2B1 Solidaire</h1>
  <p>Ensemble, nous bâtissons notre avenir.</p>
  <p>Une coopérative solidaire pour le financement local, par la communauté et pour la communauté.</p>
</header>

<section>
  <h2>Nos Services</h2>
  <div class="grid">
    <div class="card"><strong>💸 Épargne solidaire</strong><br>Cotisation régulière mensuelle</div>
    <div class="card"><strong>🔁 Crédit rotatif</strong><br>Prêts tournants entre membres</div>
    <div class="card"><strong>🛠️ Financement de projets</strong><br>Micro-financement local</div>
    <div class="card"><strong>📊 Participation aux décisions</strong><br>Assemblées ou sondages</div>
    <div class="card"><strong>📁 Espace Membre</strong></div>
    <div class="card"><strong>🧑‍🤝‍🧑 Devenir Membre</strong></div>
  </div>

  <h2>Inscription / Connexion</h2>
  <form id="registrationForm">
    <input type="text" placeholder="Nom" required>
    <input type="text" placeholder="Prénom" required>
    <input type="tel" placeholder="Téléphone" required>
    <input type="email" placeholder="Email" required>
    <input type="password" placeholder="Mot de passe" required>
    <button type="submit" class="btn">S'inscrire</button>
  </form>

  <table id="dataTable" style="display:none;">
    <thead>
      <tr><th>Nom</th><th>Prénom</th><th>Téléphone</th><th>Email</th></tr>
    </thead>
    <tbody></tbody>
  </table>

  <button class="btn" onclick="downloadCSV()" style="display:none;" id="downloadBtn">📥 Télécharger Excel</button>

  <h2>FAQ Coopérative</h2>
  <div class="grid">
    <div>• Qui peut devenir membre ?<br>• Comment les rotations fonctionnent-elles ?<br>• Que se passe-t-il si un membre ne paie pas ?</div>
    <div>• Peut-on quitter la coopérative ?<br>• Comment les décisions sont-elles prises ?<br>• Documents et règlements</div>
  </div>
</section>

<footer>
  📩 contact@d2b1solidaire.fr | <a href="#">Rejoindre la coopérative</a> | <a href="#">Voir les règles</a>
</footer>

<script>
  const form = document.getElementById('registrationForm');
  const table = document.getElementById('dataTable');
  const tbody = table.querySelector('tbody');
  const downloadBtn = document.getElementById('downloadBtn');
  const rows = [];

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    const inputs = form.querySelectorAll('input');
    const row = [inputs[0].value, inputs[1].value, inputs[2].value, inputs[3].value];
    rows.push(row);
    const tr = document.createElement('tr');
    row.forEach(cell => {
      const td = document.createElement('td');
      td.textContent = cell;
      tr.appendChild(td);
    });
    tbody.appendChild(tr);
    table.style.display = 'table';
    downloadBtn.style.display = 'inline-block';
    form.reset();
  });

  function downloadCSV() {
    let csv = 'Nom,Prénom,Téléphone,Email\n';
    rows.forEach(row => {
      csv += row.join(',') + '\n';
    });
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'inscriptions-d2b1.csv';
    a.click();
    URL.revokeObjectURL(url);
  }
</script>

</body>
</html>
